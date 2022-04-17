## Using A Shared "C" Library - Quirks And Solutions
Using a shared library is done in two steps:

1.  Compile Time - here we need to tell the linker to scan the shared library while building the executable program, so it will be convinced that no symbols are missing. It will not really take the object files from the shared library and insert them into the program.
2.  Run Time - when we run the program, we need to tell the system's dynamic loader (the process in charge of automatically loading and linking shared libraries into the running process) where to find our shared library.

The compilation part is easy. It is done almost the same as when linking with static libraries:  
  
`cc main.o -L. -lutil -o prog`  
  
The linker will look for the file 'libutil.so' (`-lutil`) in the current directory (`-L.`), and link it to the program, but will not place its object files inside the resulting executable file, 'prog'.

The run-time part is a little trickier. Normally, the system's dynamic loader looks for shared libraries in some system specified directories (such as /lib, /usr/lib, /usr/X11/lib and so on). When we build a new shared library that is not part of the system, we can use the `'LD_LIBRARY_PATH'` environment variable to tell the dynamic loader to look in other directories. The way to do that depends on the type of shell we use ('tcsh' and 'csh', versus 'sh', 'bash', 'ksh' and similar shells), as well as on whether or not `'LD_LIBRARY_PATH'` is already defined. To check if you have this variable defined, try:  
  
`echo $LD_LIBRARY_PATH`  
  
If you get a message such as `'LD_LIBRARY_PATH: Undefined variable.'`, then it is not defined.

Here is how to define this variable, in all four cases:

1.  'tcsh' or 'csh', `LD_LIBRARY_PATH` is not defined:  
    
    ```
    
        setenv LD_LIBRARY_PATH /full/path/to/library/directory
        
    ```
    
      
    
2.  'tcsh' or 'csh', `LD_LIBRARY_PATH` already defined:  
    
    ```
    
        setenv LD_LIBRARY_PATH /full/path/to/library/directory:${LD_LIBRARY_PATH}
        
    ```
    
      
    
3.  'sh', 'bash' and similar, `LD_LIBRARY_PATH` is not defined:  
    
    ```
    
        LD_LIBRARY_PATH=/full/path/to/library/directory
        export LD_LIBRARY_PATH
        
    ```
    
      
    
4.  'sh', 'bash' and similar, `LD_LIBRARY_PATH` already defined:  
    
    ```
    
        LD_LIBRARY_PATH=/full/path/to/library/directory:${LD_LIBRARY_PATH}
        export LD_LIBRARY_PATH
        
    ```
    
      
    

After you've defined `LD_LIBRARY_PATH`, you can check if the system locates the library properly for a given program linked with this library:  
  
`ldd prog`  
  
You will get a few lines, each listing a library name on the left, and a full path to the library on the right. If a library is not found in any of the system default directories, or the directories mentioned in `'LD_LIBRARY_PATH'`, you will get a 'library not found' message. In such a case, verify that you properly defined the path to the directory inside `'LD_LIBRARY_PATH'`, and fix it, if necessary. If all goes well, you can run your program now like running any other program, and see it role...

For an example of a program that uses a shared library, try looking at our [shared library example directory](https://docencia.ac.upc.edu/FIB/USO/Bibliografia/shared-lib).