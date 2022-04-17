## GCC Command Options

When you invoke GCC, it normally does preprocessing, compilation, assembly and linking. The "overall options" allow you to stop this process at an intermediate stage. For example, the `-c` option says not to run the linker. Then the output consists of object files output by the assembler.

Other options are passed on to one stage of processing. Some options control the preprocessor and others the compiler itself. Yet other options control the assembler and linker; most of these are not documented here, since you rarely need to use any of them.

Most of the command line options that you can use with GCC are useful for C programs; when an option is only useful with another language (usually C++), the explanation says so explicitly. If the description for a particular option does not mention a source language, you can use that option with all supported languages.

See [Compiling C++ Programs](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Invoking-G--.html#Invoking%20G++), for a summary of special options for compiling C++ programs.

The `gcc` program accepts options and file names as operands. Many options have multi-letter names; therefore multiple single-letter options may _not_ be grouped: `-dr` is very different from `-d -r`.

You can mix options and other arguments. For the most part, the order you use doesn't matter. Order does matter when you use several options of the same kind; for example, if you specify `-L` more than once, the directories are searched in the order specified.

Many options have long names starting with `-f` or with `-W`--for example, `-fforce-mem`, `-fstrength-reduce`, `-Wformat` and so on. Most of these have both positive and negative forms; the negative form of `-ffoo` would be `-fno-foo`. This manual documents only one of these two forms, whichever one is not the default.

See [Option Index](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Option-Index.html#Option%20Index), for an index to GCC's options.

-   [Option Summary](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Option-Summary.html#Option%20Summary): Brief list of all options, without explanations.
-   [Overall Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Overall-Options.html#Overall%20Options): Controlling the kind of output: an executable, object files, assembler files, or preprocessed source.
-   [Invoking G++](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Invoking-G--.html#Invoking%20G++): Compiling C++ programs.
-   [C Dialect Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/C-Dialect-Options.html#C%20Dialect%20Options): Controlling the variant of C language compiled.
-   [C++ Dialect Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/C---Dialect-Options.html#C++%20Dialect%20Options): Variations on C++.
-   [Objective-C Dialect Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Objective-C-Dialect-Options.html#Objective-C%20Dialect%20Options): Variations on Objective-C.
-   [Language Independent Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Language-Independent-Options.html#Language%20Independent%20Options): Controlling how diagnostics should be formatted.
-   [Warning Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Warning-Options.html#Warning%20Options): How picky should the compiler be?
-   [Debugging Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Debugging-Options.html#Debugging%20Options): Symbol tables, measurements, and debugging dumps.
-   [Optimize Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Optimize-Options.html#Optimize%20Options): How much optimization?
-   [Preprocessor Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Preprocessor-Options.html#Preprocessor%20Options): Controlling header files and macro definitions. Also, getting dependency information for Make.
-   [Assembler Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Assembler-Options.html#Assembler%20Options): Passing options to the assembler.
-   [Link Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Link-Options.html#Link%20Options): Specifying libraries and so on.
-   [Directory Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Directory-Options.html#Directory%20Options): Where to find header files and libraries. Where to find the compiler executable files.
-   [Spec Files](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Spec-Files.html#Spec%20Files): How to pass switches to sub-processes.
-   [Target Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Target-Options.html#Target%20Options): Running a cross-compiler, or an old version of GCC.
-   [Submodel Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Submodel-Options.html#Submodel%20Options): Specifying minor hardware or convention variations, such as 68010 vs 68020.
-   [Code Gen Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Code-Gen-Options.html#Code%20Gen%20Options): Specifying conventions for function calls, data layout and register usage.
-   [Environment Variables](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Environment-Variables.html#Environment%20Variables): Env vars that affect GCC.
-   [Running Protoize](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Running-Protoize.html#Running%20Protoize): Automatically adding or removing function prototypes.