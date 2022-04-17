### Options for Debugging Your Program or GCC

GCC has various special options that are used for debugging either your program or GCC:

`-g`

Produce debugging information in the operating system's native format (stabs, COFF, XCOFF, or DWARF). GDB can work with this debugging information.

On most systems that use stabs format, `-g` enables use of extra debugging information that only GDB can use; this extra information makes debugging work better in GDB but will probably make other debuggers crash or refuse to read the program. If you want to control for certain whether to generate the extra information, use `-gstabs+`, `-gstabs`, `-gxcoff+`, `-gxcoff`, `-gdwarf-1+`, `-gdwarf-1`, or `-gvms` (see below).

Unlike most other C compilers, GCC allows you to use `-g` with `-O`. The shortcuts taken by optimized code may occasionally produce surprising results: some variables you declared may not exist at all; flow of control may briefly move where you did not expect it; some statements may not be executed because they compute constant results or their values were already at hand; some statements may execute in different places because they were moved out of loops.

Nevertheless it proves possible to debug optimized output. This makes it reasonable to use the optimizer for programs that might have bugs.

The following options are useful when GCC is generated with the capability for more than one debugging format.  

`-ggdb`

Produce debugging information for use by GDB. This means to use the most expressive format available (DWARF 2, stabs, or the native format if neither of those are supported), including GDB extensions if at all possible.  

`-gstabs`

Produce debugging information in stabs format (if that is supported), without GDB extensions. This is the format used by DBX on most BSD systems. On MIPS, Alpha and System V Release 4 systems this option produces stabs debugging output which is not understood by DBX or SDB. On System V Release 4 systems this option requires the GNU assembler.  

`-gstabs+`

Produce debugging information in stabs format (if that is supported), using GNU extensions understood only by the GNU debugger (GDB). The use of these extensions is likely to make other debuggers crash or refuse to read the program.  

`-gcoff`

Produce debugging information in COFF format (if that is supported). This is the format used by SDB on most System V systems prior to System V Release 4.  

`-gxcoff`

Produce debugging information in XCOFF format (if that is supported). This is the format used by the DBX debugger on IBM RS/6000 systems.  

`-gxcoff+`

Produce debugging information in XCOFF format (if that is supported), using GNU extensions understood only by the GNU debugger (GDB). The use of these extensions is likely to make other debuggers crash or refuse to read the program, and may cause assemblers other than the GNU assembler (GAS) to fail with an error.  

`-gdwarf`

Produce debugging information in DWARF version 1 format (if that is supported). This is the format used by SDB on most System V Release 4 systems.

This option is deprecated.  

`-gdwarf+`

Produce debugging information in DWARF version 1 format (if that is supported), using GNU extensions understood only by the GNU debugger (GDB). The use of these extensions is likely to make other debuggers crash or refuse to read the program.

This option is deprecated.  

`-gdwarf-2`

Produce debugging information in DWARF version 2 format (if that is supported). This is the format used by DBX on IRIX 6.  

`-gvms`

Produce debugging information in VMS debug format (if that is supported). This is the format used by DEBUG on VMS systems.  

`-g`level

`-ggdb`level

`-gstabs`level

`-gcoff`level

`-gxcoff`level

`-gvms`level

Request debugging information and also use level to specify how much information. The default level is 2.

Level 1 produces minimal information, enough for making backtraces in parts of the program that you don't plan to debug. This includes descriptions of functions and external variables, but no information about local variables and no line numbers.

Level 3 includes extra information, such as all the macro definitions present in the program. Some debuggers support macro expansion when you use `-g3`.

Note that in order to avoid confusion between DWARF1 debug level 2, and DWARF2, neither `-gdwarf` nor `-gdwarf-2` accept a concatenated debug level. Instead use an additional `-g`level option to change the debug level for DWARF1 or DWARF2.  

`-feliminate-dwarf2-dups`

Compress DWARF2 debugging information by eliminating duplicated information about each symbol. This option only makes sense when generating DWARF2 debugging information with `-gdwarf-2`.  

`-p`

Generate extra code to write profile information suitable for the analysis program `prof`. You must use this option when compiling the source files you want data about, and you must also use it when linking.  

`-pg`

Generate extra code to write profile information suitable for the analysis program `gprof`. You must use this option when compiling the source files you want data about, and you must also use it when linking.  

`-Q`

Makes the compiler print out each function name as it is compiled, and print some statistics about each pass when it finishes.  

`-ftime-report`

Makes the compiler print some statistics about the time consumed by each pass when it finishes.  

`-fmem-report`

Makes the compiler print some statistics about permanent memory allocation when it finishes.  

`-fprofile-arcs`

Instrument arcs during compilation to generate coverage data or for profile-directed block ordering. During execution the program records how many times each branch is executed and how many times it is taken. When the compiled program exits it saves this data to a file called auxname`.da` for each source file. auxname is generated from the name of the output file, if explicitly specified and it is not the final executable, otherwise it is the basename of the source file. In both cases any suffix is removed (e.g. `foo.da` for input file `dir/foo.c`, or `dir/foo.da` for output file specified as `-o dir/foo.o`).

For profile-directed block ordering, compile the program with `-fprofile-arcs` plus optimization and code generation options, generate the arc profile information by running the program on a selected workload, and then compile the program again with the same optimization and code generation options plus `-fbranch-probabilities` (see [Options that Control Optimization](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Optimize-Options.html#Optimize%20Options)).

The other use of `-fprofile-arcs` is for use with `gcov`, when it is used with the `-ftest-coverage` option.

With `-fprofile-arcs`, for each function of your program GCC creates a program flow graph, then finds a spanning tree for the graph. Only arcs that are not on the spanning tree have to be instrumented: the compiler adds code to count the number of times that these arcs are executed. When an arc is the only exit or only entrance to a block, the instrumentation code can be added to the block; otherwise, a new basic block must be created to hold the instrumentation code.  

`-ftest-coverage`

Create data files for the `gcov` code-coverage utility (see [`gcov`--a Test Coverage Program](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Gcov.html#Gcov)). See `-fprofile-arcs` option above for a description of auxname.

auxname`.bb`

A mapping from basic blocks to line numbers, which `gcov` uses to associate basic block execution counts with line numbers.  

auxname`.bbg`

A list of all arcs in the program flow graph. This allows `gcov` to reconstruct the program flow graph, so that it can compute all basic block and arc execution counts from the information in the auxname`.da` file.

Use `-ftest-coverage` with `-fprofile-arcs`; the latter option adds instrumentation to the program, which then writes execution counts to another data file:

auxname`.da`

Runtime arc execution counts, used in conjunction with the arc information in the file auxname`.bbg`.

Coverage data will map better to the source files if `-ftest-coverage` is used without optimization.  

`-d`letters

Says to make debugging dumps during compilation at times specified by letters. This is used for debugging the compiler. The file names for most of the dumps are made by appending a pass number and a word to the dumpname. dumpname is generated from the name of the output file, if explicitly specified and it is not an executable, otherwise it is the basename of the source file. In both cases any suffix is removed (e.g. `foo.00.rtl` or `foo.01.sibling`). Here are the possible letters for use in letters, and their meanings:

`A`

Annotate the assembler output with miscellaneous debugging information.  

`b`

Dump after computing branch probabilities, to file`.14.bp`.  

`B`

Dump after block reordering, to file`.32.bbro`.  

`c`

Dump after instruction combination, to the file file`.19.combine`.  

`C`

Dump after the first if conversion, to the file file`.15.ce1`.  

`d`

Dump after delayed branch scheduling, to file`.34.dbr`.  

`D`

Dump all macro definitions, at the end of preprocessing, in addition to normal output.  

`e`

Dump after SSA optimizations, to file`.04.ssa` and file`.07.ussa`.  

`E`

Dump after the second if conversion, to file`.29.ce3`.  

`f`

Dump after control and data flow analysis, to file`.14.cfg`. Also dump after life analysis, to file`.18.life`.  

`F`

Dump after purging `ADDRESSOF` codes, to file`.10.addressof`.  

`g`

Dump after global register allocation, to file`.24.greg`.  

`G`

Dump after GCSE, to file`.11.gcse`.  

`h`

Dump after finalization of EH handling code, to file`.02.eh`.  

`i`

Dump after sibling call optimizations, to file`.01.sibling`.  

`j`

Dump after the first jump optimization, to file`.03.jump`.  

`k`

Dump after conversion from registers to stack, to file`.31.stack`.  

`l`

Dump after local register allocation, to file`.23.lreg`.  

`L`

Dump after loop optimization, to file`.12.loop`.  

`M`

Dump after performing the machine dependent reorganization pass, to file`.33.mach`.  

`n`

Dump after register renumbering, to file`.28.rnreg`.  

`N`

Dump after the register move pass, to file`.21.regmove`.  

`o`

Dump after post-reload optimizations, to file`.25.postreload`.  

`r`

Dump after RTL generation, to file`.00.rtl`.  

`R`

Dump after the second scheduling pass, to file`.30.sched2`.  

`s`

Dump after CSE (including the jump optimization that sometimes follows CSE), to file`.09.cse`.  

`S`

Dump after the first scheduling pass, to file`.22.sched`.  

`t`

Dump after the second CSE pass (including the jump optimization that sometimes follows CSE), to file`.17.cse2`.  

`T`

Dump after running tracer, to file`.16.tracer`.  

`u`

Dump after null pointer elimination pass to file`.08.null`.  

`w`

Dump after the second flow pass, to file`.26.flow2`.  

`W`

Dump after SSA conditional constant propagation, to file`.05.ssaccp`.  

`X`

Dump after SSA dead code elimination, to file`.06.ssadce`.  

`z`

Dump after the peephole pass, to file`.27.peephole2`.  

`a`

Produce all the dumps listed above.  

`m`

Print statistics on memory usage, at the end of the run, to standard error.  

`p`

Annotate the assembler output with a comment indicating which pattern and alternative was used. The length of each instruction is also printed.  

`P`

Dump the RTL in the assembler output as a comment before each instruction. Also turns on `-dp` annotation.  

`v`

For each of the other indicated dump files (except for file`.00.rtl`), dump a representation of the control flow graph suitable for viewing with VCG to file`.`pass`.vcg`.  

`x`

Just generate RTL for a function instead of compiling it. Usually used with `r`.  

`y`

Dump debugging information during parsing, to standard error.

  

`-fdump-unnumbered`

When doing debugging dumps (see `-d` option above), suppress instruction numbers and line number note output. This makes it more feasible to use diff on debugging dumps for compiler invocations with different options, in particular with and without `-g`.  

`-fdump-translation-unit` (C and C++ only)

`-fdump-translation-unit-`options (C and C++ only)

Dump a representation of the tree structure for the entire translation unit to a file. The file name is made by appending `.tu` to the source file name. If the `-`options form is used, options controls the details of the dump as described for the `-fdump-tree` options.  

`-fdump-class-hierarchy` (C++ only)

`-fdump-class-hierarchy-`options (C++ only)

Dump a representation of each class's hierarchy and virtual function table layout to a file. The file name is made by appending `.class` to the source file name. If the `-`options form is used, options controls the details of the dump as described for the `-fdump-tree` options.  

`-fdump-tree-`switch (C++ only)

`-fdump-tree-`switch`-`options (C++ only)

Control the dumping at various stages of processing the intermediate language tree to a file. The file name is generated by appending a switch specific suffix to the source file name. If the `-`options form is used, options is a list of `-` separated options that control the details of the dump. Not all options are applicable to all dumps, those which are not meaningful will be ignored. The following options are available

`address`

Print the address of each node. Usually this is not meaningful as it changes according to the environment and source file. Its primary use is for tying up a dump file with a debug environment.  

`slim`

Inhibit dumping of members of a scope or body of a function merely because that scope has been reached. Only dump such items when they are directly reachable by some other path.  

`all`

Turn on all options.

The following tree dumps are possible:

`original`

Dump before any tree based optimization, to file`.original`.  

`optimized`

Dump after all tree based optimization, to file`.optimized`.  

`inlined`

Dump after function inlining, to file`.inlined`.

  

`-frandom-seed=`string

This option provides a seed that GCC uses when it would otherwise use random numbers. At present, this is used to generate certain symbol names that have to be different in every compiled file.

The string should be different for every file you compile.  

`-fsched-verbose=`n

On targets that use instruction scheduling, this option controls the amount of debugging output the scheduler prints. This information is written to standard error, unless `-dS` or `-dR` is specified, in which case it is output to the usual dump listing file, `.sched` or `.sched2` respectively. However for n greater than nine, the output is always printed to standard error.

For n greater than zero, `-fsched-verbose` outputs the same information as `-dRS`. For n greater than one, it also output basic block probabilities, detailed ready list information and unit/insn info. For n greater than two, it includes RTL at abort point, control-flow and regions info. And for n over four, `-fsched-verbose` also includes dependence info.  

`-save-temps`

Store the usual "temporary" intermediate files permanently; place them in the current directory and name them based on the source file. Thus, compiling `foo.c` with `-c -save-temps` would produce files `foo.i` and `foo.s`, as well as `foo.o`. This creates a preprocessed `foo.i` output file even though the compiler now normally uses an integrated preprocessor.  

`-time`

Report the CPU time taken by each subprocess in the compilation sequence. For C source files, this is the compiler proper and assembler (plus the linker if linking is done). The output looks like this:

          # cc1 0.12 0.01
          # as 0.00 0.01
          

The first number on each line is the "user time," that is time spent executing the program itself. The second number is "system time," time spent executing operating system routines on behalf of the program. Both numbers are in seconds.  

`-print-file-name=`library

Print the full absolute name of the library file library that would be used when linking--and don't do anything else. With this option, GCC does not compile or link anything; it just prints the file name.  

`-print-multi-directory`

Print the directory name corresponding to the multilib selected by any other switches present in the command line. This directory is supposed to exist in `GCC_EXEC_PREFIX`.  

`-print-multi-lib`

Print the mapping from multilib directory names to compiler switches that enable them. The directory name is separated from the switches by `;`, and each switch starts with an `@` instead of the `-`, without spaces between multiple switches. This is supposed to ease shell-processing.  

`-print-prog-name=`program

Like `-print-file-name`, but searches for a program such as `cpp`.  

`-print-libgcc-file-name`

Same as `-print-file-name=libgcc.a`.

This is useful when you use `-nostdlib` or `-nodefaultlibs` but you do want to link with `libgcc.a`. You can do

          gcc -nostdlib files... `gcc -print-libgcc-file-name`
          

  

`-print-search-dirs`

Print the name of the configured installation directory and a list of program and library directories gcc will search--and don't do anything else.

This is useful when gcc prints the error message `installation problem, cannot exec cpp0: No such file or directory`. To resolve this you either need to put `cpp0` and the other compiler components where gcc expects to find them, or you can set the environment variable `GCC_EXEC_PREFIX` to the directory where you installed them. Don't forget the trailing '/'. See [Environment Variables](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Environment-Variables.html#Environment%20Variables).  

`-dumpmachine`

Print the compiler's target machine (for example, `i686-pc-linux-gnu`)--and don't do anything else.  

`-dumpversion`

Print the compiler version (for example, `3.0`)--and don't do anything else.  

`-dumpspecs`

Print the compiler's built-in specs--and don't do anything else. (This is used when GCC itself is being built.) See [Spec Files](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Spec-Files.html#Spec%20Files).