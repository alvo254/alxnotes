# File descriptor

From Wikipedia, the free encyclopedia

[Jump to navigation](https://en.wikipedia.org/wiki/File_descriptor#mw-head)[Jump to search](https://en.wikipedia.org/wiki/File_descriptor#searchInput)

In [Unix](https://en.wikipedia.org/wiki/Unix "Unix") and [Unix-like](https://en.wikipedia.org/wiki/Unix-like "Unix-like") computer operating systems, a **file descriptor** (**FD**, less frequently **fildes**) is a unique identifier ([handle](https://en.wikipedia.org/wiki/Handle_(computing) "Handle (computing)")) for a [file](https://en.wikipedia.org/wiki/File_(computing) "File (computing)") or other [input/output](https://en.wikipedia.org/wiki/Input/output "Input/output") [resource](https://en.wikipedia.org/wiki/System_resource "System resource"), such as a [pipe](https://en.wikipedia.org/wiki/Pipe_(Unix) "Pipe (Unix)") or [network socket](https://en.wikipedia.org/wiki/Network_socket "Network socket").

File descriptors typically have non-negative integer values, with negative values being reserved to indicate "no value" or error conditions.

File descriptors are a part of the [POSIX](https://en.wikipedia.org/wiki/POSIX "POSIX") [API](https://en.wikipedia.org/wiki/Application_programming_interface "Application programming interface"). Each Unix [process](https://en.wikipedia.org/wiki/Process_(computing) "Process (computing)") (except perhaps [daemons](https://en.wikipedia.org/wiki/Daemon_(computer_software) "Daemon (computer software)")) should have three standard POSIX file descriptors, corresponding to the three [standard streams](https://en.wikipedia.org/wiki/Standard_streams "Standard streams"):

Integer value

Name

<[unistd.h](https://en.wikipedia.org/wiki/Unistd.h "Unistd.h")> symbolic constant[[1]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-1)

<[stdio.h](https://en.wikipedia.org/wiki/Stdio.h "Stdio.h")> file stream[[2]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-2)

0

[Standard input](https://en.wikipedia.org/wiki/Stdin "Stdin")

STDIN_FILENO

stdin

1

[Standard output](https://en.wikipedia.org/wiki/Stdout "Stdout")

STDOUT_FILENO

stdout

2

[Standard error](https://en.wikipedia.org/wiki/Stderr "Stderr")

STDERR_FILENO

stderr

## Contents

-   [1Overview](https://en.wikipedia.org/wiki/File_descriptor#Overview)
-   [2Operations on file descriptors](https://en.wikipedia.org/wiki/File_descriptor#Operations_on_file_descriptors)
    -   [2.1Creating file descriptors](https://en.wikipedia.org/wiki/File_descriptor#Creating_file_descriptors)
    -   [2.2Deriving file descriptors](https://en.wikipedia.org/wiki/File_descriptor#Deriving_file_descriptors)
    -   [2.3Operations on a single file descriptor](https://en.wikipedia.org/wiki/File_descriptor#Operations_on_a_single_file_descriptor)
    -   [2.4Operations on multiple file descriptors](https://en.wikipedia.org/wiki/File_descriptor#Operations_on_multiple_file_descriptors)
    -   [2.5Operations on the file descriptor table](https://en.wikipedia.org/wiki/File_descriptor#Operations_on_the_file_descriptor_table)
    -   [2.6Operations that modify process state](https://en.wikipedia.org/wiki/File_descriptor#Operations_that_modify_process_state)
    -   [2.7File locking](https://en.wikipedia.org/wiki/File_descriptor#File_locking)
    -   [2.8Sockets](https://en.wikipedia.org/wiki/File_descriptor#Sockets)
    -   [2.9Miscellaneous](https://en.wikipedia.org/wiki/File_descriptor#Miscellaneous)
-   [3Upcoming operations](https://en.wikipedia.org/wiki/File_descriptor#Upcoming_operations)
-   [4File descriptors as capabilities](https://en.wikipedia.org/wiki/File_descriptor#File_descriptors_as_capabilities)
-   [5See also](https://en.wikipedia.org/wiki/File_descriptor#See_also)
-   [6References](https://en.wikipedia.org/wiki/File_descriptor#References)

## Overview[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=1 "Edit section: Overview")]

[![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f8/File_table_and_inode_table.svg/300px-File_table_and_inode_table.svg.png)](https://en.wikipedia.org/wiki/File:File_table_and_inode_table.svg)

[](https://en.wikipedia.org/wiki/File:File_table_and_inode_table.svg "Enlarge")

File descriptors for a single process, file table and [inode](https://en.wikipedia.org/wiki/Inode "Inode") table. Note that multiple file descriptors can refer to the same file table entry (e.g., as a result of the [dup](https://en.wikipedia.org/wiki/Dup_(system_call) "Dup (system call)") system call[[3]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-bach-3): 104 ) and that multiple file table entries can in turn refer to the same inode (if it has been opened multiple times; the table is still simplified because it represents inodes by file names, even though an inode can have [multiple names](https://en.wikipedia.org/wiki/Hard_link "Hard link")). File descriptor 3 does not refer to anything in the file table, signifying that it has been closed.

In the traditional implementation of Unix, file descriptors index into a per-process **file descriptor table** maintained by the kernel, that in turn indexes into a system-wide table of files opened by all processes, called the **file table**. This table records the _mode_ with which the file (or other resource) has been opened: for reading, writing, appending, and possibly other modes. It also indexes into a third table called the [inode table](https://en.wikipedia.org/wiki/Inode "Inode") that describes the actual underlying files.[[3]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-bach-3) To perform input or output, the process passes the file descriptor to the kernel through a [system call](https://en.wikipedia.org/wiki/System_call "System call"), and the kernel will access the file on behalf of the process. The process does not have direct access to the file or inode tables.

On [Linux](https://en.wikipedia.org/wiki/Linux "Linux"), the set of file descriptors open in a process can be accessed under the path `/proc/PID/fd/`, where PID is the [process identifier](https://en.wikipedia.org/wiki/Process_identifier "Process identifier"). File descriptor `/proc/PID/fd/0` is `stdin`, `/proc/PID/fd/1` is `stdout`, and `/proc/PID/fd/2` is `stderr`. As a shortcut to these, any running process can also access _its own_ file descriptors through the folders `/proc/self/fd` and `/dev/fd`.[[4]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-4)

In [Unix-like](https://en.wikipedia.org/wiki/Unix-like "Unix-like") systems, file descriptors can refer to any [Unix file type](https://en.wikipedia.org/wiki/Unix_file_type "Unix file type") named in a file system. As well as regular files, this includes [directories](https://en.wikipedia.org/wiki/Directory_(file_systems) "Directory (file systems)"), [block](https://en.wikipedia.org/wiki/Block_device "Block device") and [character devices](https://en.wikipedia.org/wiki/Character_device "Character device") (also called "special files"), [Unix domain sockets](https://en.wikipedia.org/wiki/Unix_domain_socket "Unix domain socket"), and [named pipes](https://en.wikipedia.org/wiki/Named_pipe "Named pipe"). File descriptors can also refer to other objects that do not normally exist in the file system, such as [anonymous pipes](https://en.wikipedia.org/wiki/Anonymous_pipe "Anonymous pipe") and [network sockets](https://en.wikipedia.org/wiki/Network_socket "Network socket").

The FILE data structure in the [C standard I/O library](https://en.wikipedia.org/wiki/Stdio "Stdio") usually includes a low level file descriptor for the object in question on Unix-like systems. The overall data structure provides additional abstraction and is instead known as a _file [handle](https://en.wikipedia.org/wiki/Handle_(computing) "Handle (computing)")._

## Operations on file descriptors[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=2 "Edit section: Operations on file descriptors")]

The following lists typical operations on file descriptors on modern [Unix-like](https://en.wikipedia.org/wiki/Unix-like "Unix-like") systems. Most of these functions are declared in the `<unistd.h>` header, but some are in the `<fcntl.h>` header instead.

### Creating file descriptors[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=3 "Edit section: Creating file descriptors")]

-   [open](https://en.wikipedia.org/wiki/Open_(system_call) "Open (system call)")()
-   creat()[[5]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-5)
-   socket()
-   accept()
-   socketpair()
-   pipe()
-   epoll_create() (Linux)
-   signalfd() (Linux)
-   eventfd() (Linux)
-   timerfd_create() (Linux)
-   memfd_create() (Linux)
-   userfaultfd() (Linux)
-   fanotify_init() (Linux)
-   inotify_init() (Linux)
-   clone() (with flag CLONE_PIDFD, Linux)
-   pidfd_open() (Linux)
-   open_by_handle_at() (Linux)

### Deriving file descriptors[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=4 "Edit section: Deriving file descriptors")]

-   dirfd()
-   fileno()

### Operations on a single file descriptor[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=5 "Edit section: Operations on a single file descriptor")]

-   [read](https://en.wikipedia.org/wiki/Read_(system_call) "Read (system call)")(), [write](https://en.wikipedia.org/wiki/Write_(system_call) "Write (system call)")()
-   readv(), writev()
-   pread(), pwrite()
-   recv(), send()
-   recvfrom(), sendto()
-   recvmsg(), sendmsg() (also used for sending FDs to other processes over a Unix domain socket)
-   recvmmsg(), sendmmsg()
-   lseek(), llseek()
-   [fstat()](https://en.wikipedia.org/wiki/Stat_(system_call) "Stat (system call)")
-   fstatvfs()
-   fchmod()
-   fchown()
-   ftruncate()
-   fsync()
-   fdatasync()
-   fdopendir()
-   fgetxattr(), fsetxattr() (Linux)
-   flistxattr(), fremovexattr() (Linux)
-   statx (Linux)
-   setns (Linux)
-   vmsplice() (Linux)
-   pidfd_send_signal() (Linux)
-   waitid() (with P_PIDFD ID type, Linux)
-   fdopen() (stdio function:converts file descriptor to FILE*)
-   dprintf() (stdio function: prints to file descriptor)

### Operations on multiple file descriptors[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=6 "Edit section: Operations on multiple file descriptors")]

-   [select()](https://en.wikipedia.org/wiki/Select_(Unix) "Select (Unix)"), pselect()
-   [poll()](https://en.wikipedia.org/wiki/Poll_(Unix) "Poll (Unix)"), ppoll()
-   epoll_wait(), epoll_pwait(), epoll_pwait2() (Linux, takes a single epoll filedescriptor to wait on many other file descriptors)
-   [epoll_ctl()](https://en.wikipedia.org/wiki/Epoll "Epoll") (for Linux)
-   [kqueue()](https://en.wikipedia.org/wiki/Kqueue "Kqueue") (for BSD-based systems).
-   sendfile()
-   [splice()](https://en.wikipedia.org/wiki/Splice_(system_call) "Splice (system call)"), tee() (for Linux)
-   copy_file_range() (for Linux)
-   close_range() (for Linux)[[6]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-6)

### Operations on the file descriptor table[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=7 "Edit section: Operations on the file descriptor table")]

The fcntl() function is used to perform various operations on a file descriptor, depending on the command argument passed to it. There are commands to get and set attributes associated with a file descriptor, including F_GETFD, F_SETFD, F_GETFL and F_SETFL.

-   [close()](https://en.wikipedia.org/wiki/Close_(system_call) "Close (system call)")
-   closefrom() (BSD and Solaris only; deletes all file descriptors greater than or equal to specified number)
-   [dup()](https://en.wikipedia.org/wiki/Dup_(system_call) "Dup (system call)") (duplicates an existing file descriptor guaranteeing to be the lowest number available file descriptor)
-   [dup2](https://en.wikipedia.org/wiki/Dup2 "Dup2")(), [dup3()](https://en.wikipedia.org/wiki/Dup2 "Dup2") (Close fd1 if necessary, and make file descriptor fd1 point to the open file of fd2)
-   fcntl (F_DUPFD)

### Operations that modify process state[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=8 "Edit section: Operations that modify process state")]

-   fchdir() (sets the process's current working directory based on a directory file descriptor)
-   [mmap](https://en.wikipedia.org/wiki/Mmap "Mmap")() (maps ranges of a file into the process's address space)

### File locking[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=9 "Edit section: File locking")]

-   flock()
-   fcntl() (F_GETLK, F_SETLK and F_SETLKW)
-   lockf()

### Sockets[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=10 "Edit section: Sockets")]

See also: [Berkeley sockets](https://en.wikipedia.org/wiki/Berkeley_sockets "Berkeley sockets")

-   connect()
-   bind()
-   listen()
-   accept() (creates a new file descriptor for an incoming connection)
-   getsockname()
-   getpeername()
-   getsockopt()
-   setsockopt()
-   shutdown() (shuts down one or both halves of a full duplex connection)

### Miscellaneous[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=11 "Edit section: Miscellaneous")]

-   [ioctl()](https://en.wikipedia.org/wiki/Ioctl "Ioctl") (a large collection of miscellaneous operations on a single file descriptor, often associated with a device)

## Upcoming operations[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=12 "Edit section: Upcoming operations")]

A series of new operations on file descriptors has been added to many modern Unix-like systems, as well as numerous C libraries, to be standardized in a future version of [POSIX](https://en.wikipedia.org/wiki/POSIX "POSIX").[[7]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-7) The `at` suffix signifies that the function takes an additional first argument supplying a file descriptor from which [relative paths](https://en.wikipedia.org/wiki/Relative_path "Relative path") are resolved, the forms lacking the `at` suffix thus becoming equivalent to passing a file descriptor corresponding to the current [working directory](https://en.wikipedia.org/wiki/Working_directory "Working directory"). The purpose of these new operations is to defend against a certain class of [TOCTOU](https://en.wikipedia.org/wiki/Time-of-check-to-time-of-use "Time-of-check-to-time-of-use") attacks.

-   openat()
-   faccessat()
-   fchmodat()
-   fchownat()
-   fstatat()
-   futimesat()
-   linkat()
-   mkdirat()
-   mknodat()
-   readlinkat()
-   renameat()
-   symlinkat()
-   unlinkat()
-   mkfifoat()
-   fdopendir()

## File descriptors as capabilities[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=13 "Edit section: File descriptors as capabilities")]

Unix file descriptors behave in many ways as [capabilities](https://en.wikipedia.org/wiki/Capability-based_security "Capability-based security"). They can be passed between processes across [Unix domain sockets](https://en.wikipedia.org/wiki/Unix_domain_socket "Unix domain socket") using the `[sendmsg](https://en.wikipedia.org/w/index.php?title=Sendmsg&action=edit&redlink=1 "Sendmsg (page does not exist)")()` system call. Note, however, that what is actually passed is a reference to an "open file description" that has mutable state (the file offset, and the file status and access flags). This complicates the secure use of file descriptors as capabilities, since when programs share access to the same open file description, they can interfere with each other's use of it by changing its offset or whether it is blocking or non-blocking, for example.[[8]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-8)[[9]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-9) In operating systems that are specifically designed as capability systems, there is very rarely any mutable state associated with a capability itself.

A Unix process' file descriptor table is an example of a [C-list](https://en.wikipedia.org/wiki/C-list_(computer_security) "C-list (computer security)").

## See also[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=14 "Edit section: See also")]

-   [fuser (Unix)](https://en.wikipedia.org/wiki/Fuser_(Unix) "Fuser (Unix)")
-   [lsof](https://en.wikipedia.org/wiki/Lsof "Lsof")
-   [File Control Block](https://en.wikipedia.org/wiki/File_Control_Block "File Control Block") (FCB) - an alternative scheme in CP/M and early versions of DOS

## References[[edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit&section=15 "Edit section: References")]

1.  **[^](https://en.wikipedia.org/wiki/File_descriptor#cite_ref-1 "Jump up")** [The Open Group](https://en.wikipedia.org/wiki/The_Open_Group "The Open Group"). ["The Open Group Base Specifications Issue 7, IEEE Std 1003.1-2008, 2016 Edition"](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/unistd.h.html). Retrieved 2017-09-21.
2.  **[^](https://en.wikipedia.org/wiki/File_descriptor#cite_ref-2 "Jump up")** The Open Group. ["The Open Group Base Specifications Issue 7, IEEE Std 1003.1-2008, 2016 Edition"](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/stdio.h.html). <stdio.h>. Retrieved 2017-09-21.
3.  ^ [Jump up to:_**a**_](https://en.wikipedia.org/wiki/File_descriptor#cite_ref-bach_3-0) [_**b**_](https://en.wikipedia.org/wiki/File_descriptor#cite_ref-bach_3-1) Bach, Maurice J. (1986). [_The Design of the UNIX Operating System_](https://archive.org/details/designofunixoper00bach/page/92) (8 ed.). [Prentice-Hall](https://en.wikipedia.org/wiki/Prentice-Hall "Prentice-Hall"). pp. [92–96](https://archive.org/details/designofunixoper00bach/page/92). [ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier) "ISBN (identifier)") [9780132017992](https://en.wikipedia.org/wiki/Special:BookSources/9780132017992 "Special:BookSources/9780132017992").
4.  **[^](https://en.wikipedia.org/wiki/File_descriptor#cite_ref-4 "Jump up")** ["Devices - What does the output of 'll /Proc/Self/Fd/' (From 'll /Dev/Fd') mean?"](https://unix.stackexchange.com/questions/676683/what-does-the-output-of-ll-proc-self-fd-from-ll-dev-fd-mean).
5.  **[^](https://en.wikipedia.org/wiki/File_descriptor#cite_ref-5 "Jump up")** [The Open Group](https://en.wikipedia.org/wiki/The_Open_Group "The Open Group"). ["The Open Group Base Specifications Issue 7, IEEE Std 1003.1-2008, 2018 Edition – creat"](http://pubs.opengroup.org/onlinepubs/9699919799/functions/creat.html). Retrieved 2019-04-11.
6.  **[^](https://en.wikipedia.org/wiki/File_descriptor#cite_ref-6 "Jump up")** Stephen Kitt, Michael Kerrisk. ["close_range(2) — Linux manual page"](https://man7.org/linux/man-pages/man2/close_range.2.html). Retrieved 2021-03-22.
7.  **[^](https://en.wikipedia.org/wiki/File_descriptor#cite_ref-7 "Jump up")** [_Extended API Set, Part 2_](https://www2.opengroup.org/ogsys/catalog/c063). The Open Group. October 2006. [ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier) "ISBN (identifier)") [1931624674](https://en.wikipedia.org/wiki/Special:BookSources/1931624674 "Special:BookSources/1931624674").
8.  **[^](https://en.wikipedia.org/wiki/File_descriptor#cite_ref-8 "Jump up")** Brinkmann, Marcus (2009-02-04). ["Building a bridge: library API's and file descriptors?"](https://archive.today/20120730163337/http://www.eros-os.org/pipermail/cap-talk/2009-February/012137.html). _cap-talk_. Archived from [the original](http://www.eros-os.org/pipermail/cap-talk/2009-February/012137.html) on 2012-07-30. Retrieved 2017-09-21.
9.  **[^](https://en.wikipedia.org/wiki/File_descriptor#cite_ref-9 "Jump up")** de Boyne Pollard, Jonathan (2007). ["Don't set shared file descriptors to non-blocking I/O mode"](http://jdebp.eu/FGA/dont-set-shared-file-descriptors-to-non-blocking-mode.html). Retrieved 2017-09-21.

hide

-   [v](https://en.wikipedia.org/wiki/Template:Object-capability_security "Template:Object-capability security")
-   [t](https://en.wikipedia.org/wiki/Template_talk:Object-capability_security "Template talk:Object-capability security")
-   [e](https://en.wikipedia.org/w/index.php?title=Template:Object-capability_security&action=edit)

[Object-capability](https://en.wikipedia.org/wiki/Object-capability_model "Object-capability model") security

Concepts

-   [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege "Principle of least privilege") (PoLP)
-   [Confused deputy problem](https://en.wikipedia.org/wiki/Confused_deputy_problem "Confused deputy problem")
-   [Ambient authority](https://en.wikipedia.org/wiki/Ambient_authority "Ambient authority")
-   File descriptor
-   [C-list](https://en.wikipedia.org/wiki/C-list_(computer_security) "C-list (computer security)")
-   [Object-capability model](https://en.wikipedia.org/wiki/Object-capability_model "Object-capability model")
-   [Capability-based security](https://en.wikipedia.org/wiki/Capability-based_security "Capability-based security")
-   [Capability-based addressing](https://en.wikipedia.org/wiki/Capability-based_addressing "Capability-based addressing")
-   [Zooko's triangle](https://en.wikipedia.org/wiki/Zooko%27s_triangle "Zooko's triangle")
-   [Petnames](https://en.wikipedia.org/wiki/Petname "Petname")

[Operating systems](https://en.wikipedia.org/wiki/Operating_system "Operating system"), [kernels](https://en.wikipedia.org/wiki/Kernel_(operating_system) "Kernel (operating system)")

-   [Capsicum](https://en.wikipedia.org/wiki/Capsicum_(Unix) "Capsicum (Unix)")
-   [Fuchsia](https://en.wikipedia.org/wiki/Fuchsia_(operating_system) "Fuchsia (operating system)")
-   [Genode](https://en.wikipedia.org/wiki/Genode "Genode")
-   [GNOSIS](https://en.wikipedia.org/wiki/GNOSIS "GNOSIS") → [KeyKOS](https://en.wikipedia.org/wiki/KeyKOS "KeyKOS") → [EROS](https://en.wikipedia.org/wiki/EROS_(microkernel) "EROS (microkernel)") → [CapROS](https://en.wikipedia.org/wiki/CapROS "CapROS")
-   [Hydra](https://en.wikipedia.org/wiki/Hydra_(operating_system) "Hydra (operating system)")
-   [iMAX 432](https://en.wikipedia.org/wiki/IMAX_432 "IMAX 432")
-   [Midori](https://en.wikipedia.org/wiki/Midori_(operating_system) "Midori (operating system)")
-   [NLTSS](https://en.wikipedia.org/wiki/NLTSS "NLTSS")
-   [seL4](https://en.wikipedia.org/wiki/L4_microkernel_family#High_assurance:_seL4 "L4 microkernel family")

[Programming languages](https://en.wikipedia.org/wiki/Programming_language "Programming language")

-   [Cajita](https://en.wikipedia.org/wiki/Caja_project "Caja project")
-   [E](https://en.wikipedia.org/wiki/E_(programming_language) "E (programming language)")
-   [Joe-E](https://en.wikipedia.org/wiki/Joe-E "Joe-E")
-   [Joule](https://en.wikipedia.org/wiki/Joule_(programming_language) "Joule (programming language)")

[File systems](https://en.wikipedia.org/wiki/File_system "File system")

-   [Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "Tahoe-LAFS")

Specialised hardware

-   [BiiN](https://en.wikipedia.org/wiki/BiiN "BiiN")
-   [Cambridge CAP](https://en.wikipedia.org/wiki/CAP_computer "CAP computer")
-   [Flex](https://en.wikipedia.org/wiki/Flex_machine "Flex machine")
-   [IBM System/38](https://en.wikipedia.org/wiki/IBM_System/38 "IBM System/38")
-   [Intel iAPX 432](https://en.wikipedia.org/wiki/Intel_iAPX_432 "Intel iAPX 432")
-   [Plessey System 250](https://en.wikipedia.org/wiki/Plessey_System_250 "Plessey System 250")

[Categories](https://en.wikipedia.org/wiki/Help:Category "Help:Category"): 

-   [POSIX](https://en.wikipedia.org/wiki/Category:POSIX "Category:POSIX")
-   [Unix file system technology](https://en.wikipedia.org/wiki/Category:Unix_file_system_technology "Category:Unix file system technology")

## Navigation menu

-   Not logged in
-   [Talk](https://en.wikipedia.org/wiki/Special:MyTalk "Discussion about edits from this IP address [alt-shift-n]")
-   [Contributions](https://en.wikipedia.org/wiki/Special:MyContributions "A list of edits made from this IP address [alt-shift-y]")
-   [Create account](https://en.wikipedia.org/w/index.php?title=Special:CreateAccount&returnto=File+descriptor "You are encouraged to create an account and log in; however, it is not mandatory")
-   [Log in](https://en.wikipedia.org/w/index.php?title=Special:UserLogin&returnto=File+descriptor "You're encouraged to log in; however, it's not mandatory. [alt-shift-o]")

-   [Article](https://en.wikipedia.org/wiki/File_descriptor "View the content page [alt-shift-c]")
-   [Talk](https://en.wikipedia.org/wiki/Talk:File_descriptor "Discuss improvements to the content page [alt-shift-t]")

-   [Read](https://en.wikipedia.org/wiki/File_descriptor)
-   [Edit](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=edit "Edit this page [alt-shift-e]")
-   [View history](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=history "Past revisions of this page [alt-shift-h]")

### Search

[](https://en.wikipedia.org/wiki/Main_Page "Visit the main page")

-   [Main page](https://en.wikipedia.org/wiki/Main_Page "Visit the main page [alt-shift-z]")
-   [Contents](https://en.wikipedia.org/wiki/Wikipedia:Contents "Guides to browsing Wikipedia")
-   [Current events](https://en.wikipedia.org/wiki/Portal:Current_events "Articles related to current events")
-   [Random article](https://en.wikipedia.org/wiki/Special:Random "Visit a randomly selected article [alt-shift-x]")
-   [About Wikipedia](https://en.wikipedia.org/wiki/Wikipedia:About "Learn about Wikipedia and how it works")
-   [Contact us](https://en.wikipedia.org/wiki/Wikipedia:Contact_us "How to contact Wikipedia")
-   [Donate](https://donate.wikimedia.org/wiki/Special:FundraiserRedirector?utm_source=donate&utm_medium=sidebar&utm_campaign=C13_en.wikipedia.org&uselang=en "Support us by donating to the Wikimedia Foundation")

Contribute

-   [Help](https://en.wikipedia.org/wiki/Help:Contents "Guidance on how to use and edit Wikipedia")
-   [Learn to edit](https://en.wikipedia.org/wiki/Help:Introduction "Learn how to edit Wikipedia")
-   [Community portal](https://en.wikipedia.org/wiki/Wikipedia:Community_portal "The hub for editors")
-   [Recent changes](https://en.wikipedia.org/wiki/Special:RecentChanges "A list of recent changes to Wikipedia [alt-shift-r]")
-   [Upload file](https://en.wikipedia.org/wiki/Wikipedia:File_Upload_Wizard "Add images or other media for use on Wikipedia")

Tools

-   [What links here](https://en.wikipedia.org/wiki/Special:WhatLinksHere/File_descriptor "List of all English Wikipedia pages containing links to this page [alt-shift-j]")
-   [Related changes](https://en.wikipedia.org/wiki/Special:RecentChangesLinked/File_descriptor "Recent changes in pages linked from this page [alt-shift-k]")
-   [Special pages](https://en.wikipedia.org/wiki/Special:SpecialPages "A list of all special pages [alt-shift-q]")
-   [Permanent link](https://en.wikipedia.org/w/index.php?title=File_descriptor&oldid=1085242585 "Permanent link to this revision of this page")
-   [Page information](https://en.wikipedia.org/w/index.php?title=File_descriptor&action=info "More information about this page")
-   [Cite this page](https://en.wikipedia.org/w/index.php?title=Special:CiteThisPage&page=File_descriptor&id=1085242585&wpFormIdentifier=titleform "Information on how to cite this page")
-   [Wikidata item](https://www.wikidata.org/wiki/Special:EntityPage/Q1060813 "Structured data on this page hosted by Wikidata [alt-shift-g]")

Print/export

-   [Download as PDF](https://en.wikipedia.org/w/index.php?title=Special:DownloadAsPdf&page=File_descriptor&action=show-download-screen "Download this page as a PDF file")
-   [Printable version](https://en.wikipedia.org/w/index.php?title=File_descriptor&printable=yes "Printable version of this page [alt-shift-p]")

Languages

-   [Deutsch](https://de.wikipedia.org/wiki/Handle#Datei-Handle "Handle – German")
-   [Español](https://es.wikipedia.org/wiki/Descriptor_de_archivo "Descriptor de archivo – Spanish")
-   [Français](https://fr.wikipedia.org/wiki/Descripteur_de_fichier "Descripteur de fichier – French")
-   [한국어](https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%9D%BC_%EC%84%9C%EC%88%A0%EC%9E%90 "파일 서술자 – Korean")
-   [日本語](https://ja.wikipedia.org/wiki/%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E8%A8%98%E8%BF%B0%E5%AD%90 "ファイル記述子 – Japanese")
-   [Português](https://pt.wikipedia.org/wiki/Descritor_de_arquivo "Descritor de arquivo – Portuguese")
-   [Русский](https://ru.wikipedia.org/wiki/%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D0%B9_%D0%B4%D0%B5%D1%81%D0%BA%D1%80%D0%B8%D0%BF%D1%82%D0%BE%D1%80 "Файловый дескриптор – Russian")
-   [Tiếng Việt](https://vi.wikipedia.org/wiki/%C4%90%E1%BA%B7c_t%E1%BA%A3_t%E1%BA%ADp_tin "Đặc tả tập tin – Vietnamese")
-   [中文](https://zh.wikipedia.org/wiki/%E6%96%87%E4%BB%B6%E6%8F%8F%E8%BF%B0%E7%AC%A6 "文件描述符 – Chinese")
8 more

[Edit links](https://www.wikidata.org/wiki/Special:EntityPage/Q1060813#sitelinks-wikipedia "Edit interlanguage links")