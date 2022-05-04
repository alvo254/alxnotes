For most [file systems](https://en.wikipedia.org/wiki/File_system "File system"), a [program](https://en.wikipedia.org/wiki/Computer_program "Computer program") initializes access to a [file](https://en.wikipedia.org/wiki/Computer_file "Computer file") in a [file system](https://en.wikipedia.org/wiki/File_system "File system") using the **open** [system call](https://en.wikipedia.org/wiki/System_call "System call"). This allocates resources associated to the file (the [file descriptor](https://en.wikipedia.org/wiki/File_descriptor "File descriptor")), and returns a [handle](https://en.wikipedia.org/wiki/Smart_pointer#Handles "Smart pointer") that the [process](https://en.wikipedia.org/wiki/Process_(computing) "Process (computing)") will use to refer to that file. In some cases the open is performed by the first access.

The same file may be opened simultaneously by several processes, and even by the same process, resulting in several file descriptors for the same file; depending on the file organization and filesystem. Operations on the descriptors such as moving the [file pointer](https://en.wikipedia.org/wiki/FILE_pointer "FILE pointer") or closing it are independent—they do not affect other descriptors for the same file. Operations on the file, such as a [write](https://en.wikipedia.org/wiki/Write_(system_call) "Write (system call)"), can be seen by operations on the other descriptors: a later read can read the newly written data.

During the `open`, the filesystem may allocate memory for [buffers](https://en.wikipedia.org/wiki/Data_buffer "Data buffer"), or it may wait until the first operation.

The [absolute file path](https://en.wikipedia.org/wiki/File_path#Absolute_and_relative_paths "File path") is resolved. This may include connecting to a remote host and notifying an operator that a removable medium is required. It may include the initialization of a communication device. At this point an error may be returned if the host or medium is not available. The first access to at least the [directory](https://en.wikipedia.org/wiki/Directory_(computing) "Directory (computing)") within the filesystem is performed. An error will usually be returned if the higher level components of the path ([directories](https://en.wikipedia.org/wiki/Directory_(computing) "Directory (computing)")) cannot be located or accessed. An error will be returned if the file is expected to exist and it does not or if the file should not already exist and it does.

If the file is expected to exist and it does, the file access, as restricted by [permission flags](https://en.wikipedia.org/wiki/File_system_permissions "File system permissions") within the file meta data or [access control list](https://en.wikipedia.org/wiki/Access_control_list "Access control list"), is validated against the requested type of operations. This usually requires an additional filesystem access although in some filesystems meta-flags may be part of the directory structure.

If the file is being created, the filesystem may allocate the default initial amount of storage or a specified amount depending on the file system capabilities. If this fails an error will be returned. Updating the directory with the new entry may be performed or it may be delayed until the [close](https://en.wikipedia.org/wiki/Close_(system_call) "Close (system call)") is performed.

Various other errors which may occur during the open include directory update failures, un-permitted multiple connections, media failures, communication link failures and device failures.

The return value must always be examined and an error specific action taken.

In many cases programming language-specific run-time library opens may perform additional actions including initializing a run-time library structure related to the file.

As soon as a file is no longer needed, the program should close it. This will cause run-time library and filesystem buffers to be updated to the physical media and permit other processes to access the data if exclusive use had been required. Some run-time libraries may close a file if the program calls the run-time exit. Some filesystems may perform the necessary operations if the program terminates. Neither of these is likely to take place in the event of a kernel or power failure. This can cause damaged filesystem structures requiring the running of privileged and lengthy filesystem utilities during which the entire filesystem may be inaccessible.

## Contents

-   [1open call arguments](https://en.wikipedia.org/wiki/Open_(system_call)#open_call_arguments)
    -   [1.1Perl language form](https://en.wikipedia.org/wiki/Open_(system_call)#Perl_language_form)
    -   [1.2C library POSIX definition](https://en.wikipedia.org/wiki/Open_(system_call)#C_library_POSIX_definition)
        -   [1.2.1path](https://en.wikipedia.org/wiki/Open_(system_call)#path)
        -   [1.2.2oflag](https://en.wikipedia.org/wiki/Open_(system_call)#oflag)
        -   [1.2.3mode](https://en.wikipedia.org/wiki/Open_(system_call)#mode)
-   [2See also](https://en.wikipedia.org/wiki/Open_(system_call)#See_also)
-   [3Notes](https://en.wikipedia.org/wiki/Open_(system_call)#Notes)
-   [4References](https://en.wikipedia.org/wiki/Open_(system_call)#References)

## open call arguments[[edit](https://en.wikipedia.org/w/index.php?title=Open_(system_call)&action=edit&section=1 "Edit section: open call arguments")]

1.  The [pathname](https://en.wikipedia.org/wiki/Pathname "Pathname") to the file,
2.  The kind of access requested on the file (read, write, append etc.),
3.  The initial file permission is requested using the third argument called `mode`. This argument is relevant only when a new file is being created.

After using the file, the process should close the file using [close](https://en.wikipedia.org/wiki/Close_(system_call) "Close (system call)") call, which takes the file descriptor of the file to be closed. Some filesystems include a disposition to permit releasing the file.

Some computer languages include run-time libraries which include additional functionality for particular filesystems. The open (or some auxiliary routine) may include specifications for key size, record size, connection speed. Some open routines include specification of the program code to be executed in the event of an error.

### Perl language form[[edit](https://en.wikipedia.org/w/index.php?title=Open_(system_call)&action=edit&section=2 "Edit section: Perl language form")]

open FILEHANDLE,MODE[,EXPR]

for example:

open(my $fh, ">", "output.txt");

[Perl](https://en.wikipedia.org/wiki/Perl "Perl") also uses the `tie` function of the `Tie::File` module to associate an array with a file.[[1]](https://en.wikipedia.org/wiki/Open_(system_call)#cite_note-perlTieArray-1) The `tie::AnyDBM_File` function associates a hash with a file.[[2]](https://en.wikipedia.org/wiki/Open_(system_call)#cite_note-perlTieHash-2)

### C library POSIX definition[[edit](https://en.wikipedia.org/w/index.php?title=Open_(system_call)&action=edit&section=3 "Edit section: C library POSIX definition")]

The [open](http://pubs.opengroup.org/onlinepubs/9699919799/functions/open.html) call is standardized by the [POSIX](https://en.wikipedia.org/wiki/POSIX "POSIX") specification for [C language](https://en.wikipedia.org/wiki/C_(programming_language) "C (programming language)"):

int open(const char *path, int oflag, .../*,mode_t mode */);
int openat(int fd, const char *path, int oflag, ...);
int creat(const char *path, mode_t mode);
FILE *fopen(const char *restrict filename, const char *restrict mode);

The value returned is a file descriptor which is a reference to a process specific structure which contains, among other things, a position pointer that indicates which place in the file will be acted upon by the next operation.

Open may return [−1](https://en.wikipedia.org/wiki/%E2%88%921 "−1") indicating a failure with `errno` detailing the error.

The file system also updates a global table of all open files which is used for determining if a file is currently in use by any process.

#### path[[edit](https://en.wikipedia.org/w/index.php?title=Open_(system_call)&action=edit&section=4 "Edit section: path")]

The name of the file to open. It includes the [file path](https://en.wikipedia.org/wiki/File_path "File path") defining where, in which file system, the file is found (or should be created).

`openat` expects a relative path.

#### oflag[[edit](https://en.wikipedia.org/w/index.php?title=Open_(system_call)&action=edit&section=5 "Edit section: oflag")]

This argument formed by [OR'ing together](https://en.wikipedia.org/wiki/Mask_(computing)#Arguments_to_functions "Mask (computing)") optional parameters and (from <[fcntl.h](https://en.wikipedia.org/wiki/Fcntl.h "Fcntl.h")>) one of:

`O_RDONLY`, `O_RDWR` and `O_WRONLY`

Option parameters include:

`O_APPEND` data written will be appended to the end of the file. The file operations will always adjust the position pointer to the end of the file.

`O_CREAT` Create the file if it does not exist; otherwise the open fails setting [errno](https://en.wikipedia.org/wiki/Errno "Errno") to ENOENT.

`O_EXCL` Used with `O_CREAT` if the file already exists, then fail, setting errno to EEXIST.

`O_TRUNC` If the file already exists then discard its previous contents, reducing it to an empty file. Not applicable for a device or named pipe.

Additional flags and errors are defined in [open](http://pubs.opengroup.org/onlinepubs/9699919799/functions/open.html) call.

`creat()` is implemented as:

int creat(const char *path, mode_t mode)
{
    return open(path, O_WRONLY|O_CREAT|O_TRUNC, mode);
}

[fopen](http://pubs.opengroup.org/onlinepubs/9699919799/functions/fopen.html) uses string flags such as `r`, `w`, `a` and `+` and returns a file pointer used with [fgets](http://pubs.opengroup.org/onlinepubs/9699919799/functions/fgets.html), [fputs](http://pubs.opengroup.org/onlinepubs/9699919799/functions/fputs.html) and [fclose](http://pubs.opengroup.org/onlinepubs/9699919799/functions/fclose.html).

#### mode[[edit](https://en.wikipedia.org/w/index.php?title=Open_(system_call)&action=edit&section=6 "Edit section: mode")]

Optional and relevant only when creating a new file, defines the [file permissions](https://en.wikipedia.org/wiki/File_permissions "File permissions"). These include read, write or execute the file by the owner, group or all users. The mode is masked by the calling process's [umask](https://en.wikipedia.org/wiki/Umask "Umask"): bits set in the umask are cleared in the mode.

## See also[[edit](https://en.wikipedia.org/w/index.php?title=Open_(system_call)&action=edit&section=7 "Edit section: See also")]

-   [File descriptor](https://en.wikipedia.org/wiki/File_descriptor "File descriptor") – how it works and other functions related to `open`

## Notes[[edit](https://en.wikipedia.org/w/index.php?title=Open_(system_call)&action=edit&section=8 "Edit section: Notes")]

1.  **[^](https://en.wikipedia.org/wiki/Open_(system_call)#cite_ref-perlTieArray_1-0 "Jump up")** ["Tie::File"](http://perldoc.perl.org/Tie/File.html). perldoc.perl.org. Retrieved 2011-08-07.
2.  **[^](https://en.wikipedia.org/wiki/Open_(system_call)#cite_ref-perlTieHash_2-0 "Jump up")** ["AnyDBM_File"](http://perldoc.perl.org/AnyDBM_File.html). perldoc.perl.org. Retrieved 2011-08-07.

## References[[edit](https://en.wikipedia.org/w/index.php?title=Open_(system_call)&action=edit&section=9 "Edit section: References")]

-   Advanced Programming in the UNIX Environment by W. Richard Stevens [ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier) "ISBN (identifier)") [81-7808-096-6](https://en.wikipedia.org/wiki/Special:BookSources/81-7808-096-6 "Special:BookSources/81-7808-096-6")
-   UNIX concept & application by Sumitabh Das

  

hide

-   [v](https://en.wikipedia.org/wiki/Template:Computer_files "Template:Computer files")
-   [t](https://en.wikipedia.org/wiki/Template_talk:Computer_files "Template talk:Computer files")
-   [e](https://en.wikipedia.org/w/index.php?title=Template:Computer_files&action=edit)

[Computer files](https://en.wikipedia.org/wiki/Computer_file "Computer file")

Types

-   [Binary file](https://en.wikipedia.org/wiki/Binary_file "Binary file") / [text file](https://en.wikipedia.org/wiki/Text_file "Text file")
-   [File format](https://en.wikipedia.org/wiki/File_format "File format") 
    -   [List of file formats](https://en.wikipedia.org/wiki/List_of_file_formats "List of file formats")
    -   [File signatures](https://en.wikipedia.org/wiki/List_of_file_signatures "List of file signatures")
    -   [Magic number](https://en.wikipedia.org/wiki/Magic_number_(programming) "Magic number (programming)")
-   [Metafile](https://en.wikipedia.org/wiki/Metafile "Metafile")
-   [Sidecar file](https://en.wikipedia.org/wiki/Sidecar_file "Sidecar file")
-   [Sparse file](https://en.wikipedia.org/wiki/Sparse_file "Sparse file")
-   [Swap file](https://en.wikipedia.org/wiki/Swap_file "Swap file")
-   [System file](https://en.wikipedia.org/wiki/System_file "System file")
-   [Temporary file](https://en.wikipedia.org/wiki/Temporary_file "Temporary file")
-   [Zero-byte file](https://en.wikipedia.org/wiki/Zero-byte_file "Zero-byte file")

Properties

-   [Filename](https://en.wikipedia.org/wiki/Filename "Filename") 
    -   [8.3 filename](https://en.wikipedia.org/wiki/8.3_filename "8.3 filename")
    -   [Long filename](https://en.wikipedia.org/wiki/Long_filename "Long filename")
    -   [Filename mangling](https://en.wikipedia.org/wiki/Filename_mangling "Filename mangling")
-   [Filename extension](https://en.wikipedia.org/wiki/Filename_extension "Filename extension") 
    -   [List of filename extensions](https://en.wikipedia.org/wiki/List_of_filename_extensions "List of filename extensions")
-   [File attribute](https://en.wikipedia.org/wiki/File_attribute "File attribute") 
    -   [Extended file attributes](https://en.wikipedia.org/wiki/Extended_file_attributes "Extended file attributes")
-   [File size](https://en.wikipedia.org/wiki/File_size "File size")
-   [Hidden file / Hidden directory](https://en.wikipedia.org/wiki/Hidden_file_and_hidden_directory "Hidden file and hidden directory")

Organisation

-   [Directory/folder](https://en.wikipedia.org/wiki/Directory_(computing) "Directory (computing)") 
    -   [NTFS links](https://en.wikipedia.org/wiki/NTFS_links "NTFS links")
    -   [Temporary folder](https://en.wikipedia.org/wiki/Temporary_folder "Temporary folder")
-   [Directory structure](https://en.wikipedia.org/wiki/Directory_structure "Directory structure")
-   [File sequence](https://en.wikipedia.org/wiki/File_sequence "File sequence")
-   [File system](https://en.wikipedia.org/wiki/File_system "File system") 
    -   [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard "Filesystem Hierarchy Standard")
-   [Path](https://en.wikipedia.org/wiki/Path_(computing) "Path (computing)")

[Operations](https://en.wikipedia.org/wiki/File_operation "File operation")

-   Open
-   [Close](https://en.wikipedia.org/wiki/Close_(system_call) "Close (system call)")
-   [Read](https://en.wikipedia.org/wiki/Read_(system_call) "Read (system call)")
-   [Write](https://en.wikipedia.org/wiki/Write_(system_call) "Write (system call)")

Linking

-   [File descriptor](https://en.wikipedia.org/wiki/File_descriptor "File descriptor")
-   [Hard link](https://en.wikipedia.org/wiki/Hard_link "Hard link")
-   [Shortcut](https://en.wikipedia.org/wiki/Shortcut_(computing) "Shortcut (computing)") 
    -   [Alias](https://en.wikipedia.org/wiki/Alias_(Mac_OS) "Alias (Mac OS)")
    -   [Shadow](https://en.wikipedia.org/wiki/Shadow_(OS/2) "Shadow (OS/2)")
-   [Symbolic link](https://en.wikipedia.org/wiki/Symbolic_link "Symbolic link")

Management

-   [File comparison](https://en.wikipedia.org/wiki/File_comparison "File comparison")
-   [Data compression](https://en.wikipedia.org/wiki/Data_compression "Data compression")
-   [File manager](https://en.wikipedia.org/wiki/File_manager "File manager") 
    -   [Comparison of file managers](https://en.wikipedia.org/wiki/Comparison_of_file_managers "Comparison of file managers")
-   [File system permissions](https://en.wikipedia.org/wiki/File_system_permissions "File system permissions")
-   [File transfer](https://en.wikipedia.org/wiki/File_transfer "File transfer") 
    -   [File sharing](https://en.wikipedia.org/wiki/File_sharing "File sharing")
-   [File verification](https://en.wikipedia.org/wiki/File_verification "File verification")

[Categories](https://en.wikipedia.org/wiki/Help:Category "Help:Category"): 

-   [C POSIX library](https://en.wikipedia.org/wiki/Category:C_POSIX_library "Category:C POSIX library")
-   [System calls](https://en.wikipedia.org/wiki/Category:System_calls "Category:System calls")