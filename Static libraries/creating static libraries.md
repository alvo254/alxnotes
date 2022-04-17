## Creating A Static "C" Library Using "ar" and "ranlib"

The basic tool used to create static libraries is a program called `'ar'`, for 'archiver'. This program can be used to create static libraries (which are actually archive files), modify object files in the static library, list the names of object files in the library, and so on. In order to create a static library, we can use a command like this:  
  
`ar rc libutil.a util_file.o util_net.o util_math.o`  
  
This command creates a static library named 'libutil.a' and puts copies of the object files "util_file.o", "util_net.o" and "util_math.o" in it. If the library file already exists, it has the object files added to it, or replaced, if they are newer than those inside the library. The `'c'` flag tells ar to create the library if it doesn't already exist. The `'r'` flag tells it to replace older object files in the library, with the new object files.

After an archive is created, or modified, there is a need to index it. This index is later used by the compiler to speed up symbol-lookup inside the library, and to make sure that the order of the symbols in the library won't matter during compilation (this will be better understood when we take a deeper look at the link process at the end of this tutorial). The command used to create or update the index is called `'ranlib'`, and is invoked as follows:  
  
`ranlib libutil.a`  
  
On some systems, the archiver (which is not always `ar`) already takes care of the index, so ranlib is not needed (for example, when Sun's C compiler creates an archive, it is already indexed). However, because `'ar'` and `'ranlib'` are used by many makefiles for many packages, such platforms tend to supply a ranlib command that does nothing. This helps using the same makefile on both types of platforms.

_Note_: when an archive file's index generation date (stored inside the archive file) is older than the file's last modification date (stored in the file system), a compiler trying to use this library will complain its index is out of date, and abort. There are two ways to overcome the problem:

1.  Use `'ranlib'` to re-generate the index.
2.  When copying the archive file to another location, use `'cp -p'`, instead of only `'cp'`. The `'-p'` flag tells `'cp'` to keep all attributes of the file, including its access permissions, owner (if "cp" is invoked by a superuser) and its last modification date. This will cause the compiler to think the index inside the file is still updated. This method is useful for makefiles that need to copy the library to another directory for some reason.

---