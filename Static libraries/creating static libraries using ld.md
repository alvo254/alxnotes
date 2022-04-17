## Creating A Shared "C" Library Using "ld"

The creation of a shared library is rather similar to the creation of a static library. Compile a list of object files, then insert them all into a shared library file. However, there are two major differences:

1.  Compile for "Position Independent Code" (PIC) - When the object files are generated, we have no idea where in memory they will be inserted in a program that will use them. Many different programs may use the same library, and each load it into a different memory in address. Thus, we need that all jump calls ("goto", in assembly speak) and subroutine calls will use relative addresses, and not absolute addresses. Thus, we need to use a compiler flag that will cause this type of code to be generated.  
    In most compilers, this is done by specifying `'-fPIC'` or `'-fpic'` on the compilation command.
2.  Library File Creation - unlike a static library, a shared library is not an archive file. It has a format that is specific to the architecture for which it is being created. Thus, we need to use the compiler (either the compiler's driver, or its linker) to generate the library, and tell it that it should create a shared library, not a final program file.  
    This is done by using the `'-G'` flag with some compilers, or the `'-shared'` flag with other compilers.

Thus, the set of commands we will use to create a shared library, would be something like this:  

```

cc -fPIC -c util_file.c
cc -fPIC -c util_net.c
cc -fPIC -c util_math.c
cc -shared libutil.so util_file.o util_net.o util_math.o
```

  
The first three commands compile the source files with the `PIC` option, so they will be suitable for use in a shared library (they may still be used in a program directly, even thought they were compiled with `PIC`). The last command asks the compiler to generate a shared library