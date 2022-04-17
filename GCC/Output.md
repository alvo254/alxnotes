### Options Controlling the Kind of Output

Compilation can involve up to four stages: preprocessing, compilation proper, assembly and linking, always in that order. The first three stages apply to an individual source file, and end by producing an object file; linking combines all the object files (those newly compiled, and those specified as input) into an executable file.

For any given input file, the file name suffix determines what kind of compilation is done:

file`.c`

C source code which must be preprocessed.  

file`.i`

C source code which should not be preprocessed.  

file`.ii`

C++ source code which should not be preprocessed.  

file`.m`

Objective-C source code. Note that you must link with the library `libobjc.a` to make an Objective-C program work.  

file`.mi`

Objective-C source code which should not be preprocessed.  

file`.h`

C header file (not to be compiled or linked).  

file`.cc`

file`.cp`

file`.cxx`

file`.cpp`

file`.c++`

file`.C`

C++ source code which must be preprocessed. Note that in `.cxx`, the last two letters must both be literally `x`. Likewise, `.C` refers to a literal capital C.  

file`.f`

file`.for`

file`.FOR`

Fortran source code which should not be preprocessed.  

file`.F`

file`.fpp`

file`.FPP`

Fortran source code which must be preprocessed (with the traditional preprocessor).  

file`.r`

Fortran source code which must be preprocessed with a RATFOR preprocessor (not included with GCC).

See [Options Controlling the Kind of Output](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/g77/Overall-Options.html#Overall%20Options), for more details of the handling of Fortran input files.  

file`.ads`

Ada source code file which contains a library unit declaration (a declaration of a package, subprogram, or generic, or a generic instantiation), or a library unit renaming declaration (a package, generic, or subprogram renaming declaration). Such files are also called specs.

file`.adb`

Ada source code file containing a library unit body (a subprogram or package body). Such files are also called bodies.  

file`.s`

Assembler code.  

file`.S`

Assembler code which must be preprocessed.  

other

An object file to be fed straight into linking. Any file name with no recognized suffix is treated this way.

You can specify the input language explicitly with the `-x` option:

`-x` language

Specify explicitly the language for the following input files (rather than letting the compiler choose a default based on the file name suffix). This option applies to all following input files until the next `-x` option. Possible values for language are:

          c  c-header  cpp-output
          c++  c++-cpp-output
          objective-c  objc-cpp-output
          assembler  assembler-with-cpp
          ada
          f77  f77-cpp-input  ratfor
          java
          treelang
          

  

`-x none`

Turn off any specification of a language, so that subsequent files are handled according to their file name suffixes (as they are if `-x` has not been used at all).  

`-pass-exit-codes`

Normally the `gcc` program will exit with the code of 1 if any phase of the compiler returns a non-success return code. If you specify `-pass-exit-codes`, the `gcc` program will instead return with numerically highest error produced by any phase that returned an error indication.

If you only want some of the stages of compilation, you can use `-x` (or filename suffixes) to tell `gcc` where to start, and one of the options `-c`, `-S`, or `-E` to say where `gcc` is to stop. Note that some combinations (for example, `-x cpp-output -E`) instruct `gcc` to do nothing at all.

`-c`

Compile or assemble the source files, but do not link. The linking stage simply is not done. The ultimate output is in the form of an object file for each source file.

By default, the object file name for a source file is made by replacing the suffix `.c`, `.i`, `.s`, etc., with `.o`.

Unrecognized input files, not requiring compilation or assembly, are ignored.  

`-S`

Stop after the stage of compilation proper; do not assemble. The output is in the form of an assembler code file for each non-assembler input file specified.

By default, the assembler file name for a source file is made by replacing the suffix `.c`, `.i`, etc., with `.s`.

Input files that don't require compilation are ignored.  

`-E`

Stop after the preprocessing stage; do not run the compiler proper. The output is in the form of preprocessed source code, which is sent to the standard output.

Input files which don't require preprocessing are ignored.  

`-o` file

Place output in file file. This applies regardless to whatever sort of output is being produced, whether it be an executable file, an object file, an assembler file or preprocessed C code.

Since only one output file can be specified, it does not make sense to use `-o` when compiling more than one input file, unless you are producing an executable file as output.

If `-o` is not specified, the default is to put an executable file in `a.out`, the object file for source`.`suffix in source`.o`, its assembler file in source`.s`, and all preprocessed C source on standard output.  

`-v`

Print (on standard error output) the commands executed to run the stages of compilation. Also print the version number of the compiler driver program and of the preprocessor and the compiler proper.  

`-###`

Like `-v` except the commands are not executed and all command arguments are quoted. This is useful for shell scripts to capture the driver-generated command lines.  

`-pipe`

Use pipes rather than temporary files for communication between the various stages of compilation. This fails to work on some systems where the assembler is unable to read from a pipe; but the GNU assembler has no trouble.  

`--help`

Print (on the standard output) a description of the command line options understood by `gcc`. If the `-v` option is also specified then `--help` will also be passed on to the various processes invoked by `gcc`, so that they can display the command line options they accept. If the `-W` option is also specified then command line options which have no documentation associated with them will also be displayed.  

`--target-help`

Print (on the standard output) a description of target specific command line options for each tool.  

`--version`

Display the version number and copyrights of the invoked GCC.