### Options That Control Optimization

These options control various sorts of optimizations.

Without any optimization option, the compiler's goal is to reduce the cost of compilation and to make debugging produce the expected results. Statements are independent: if you stop the program with a breakpoint between statements, you can then assign a new value to any variable or change the program counter to any other statement in the function and get exactly the results you would expect from the source code.

Turning on optimization flags makes the compiler attempt to improve the performance and/or code size at the expense of compilation time and possibly the ability to debug the program.

Not all optimizations are controlled directly by a flag. Only optimizations that have a flag are listed.

`-O`

`-O1`

Optimize. Optimizing compilation takes somewhat more time, and a lot more memory for a large function.

With `-O`, the compiler tries to reduce code size and execution time, without performing any optimizations that take a great deal of compilation time.

`-O` turns on the following optimization flags:

          -fdefer-pop 
          -fmerge-constants 
          -fthread-jumps 
          -floop-optimize 
          -fcrossjumping 
          -fif-conversion 
          -fif-conversion2 
          -fdelayed-branch 
          -fguess-branch-probability 
          -fcprop-registers
          

`-O` also turns on `-fomit-frame-pointer` on machines where doing so does not interfere with debugging.  

`-O2`

Optimize even more. GCC performs nearly all supported optimizations that do not involve a space-speed tradeoff. The compiler does not perform loop unrolling or function inlining when you specify `-O2`. As compared to `-O`, this option increases both compilation time and the performance of the generated code.

`-O2` turns on all optimization flags specified by `-O`. It also turns on the following optimization flags:

          -fforce-mem 
          -foptimize-sibling-calls 
          -fstrength-reduce 
          -fcse-follow-jumps  -fcse-skip-blocks 
          -frerun-cse-after-loop  -frerun-loop-opt 
          -fgcse   -fgcse-lm   -fgcse-sm 
          -fdelete-null-pointer-checks 
          -fexpensive-optimizations 
          -fregmove 
          -fschedule-insns  -fschedule-insns2 
          -fsched-interblock -fsched-spec 
          -fcaller-saves 
          -fpeephole2 
          -freorder-blocks  -freorder-functions 
          -fstrict-aliasing 
          -falign-functions  -falign-jumps 
          -falign-loops  -falign-labels
          

Please note the warning under `-fgcse` about invoking `-O2` on programs that use computed gotos.  

`-O3`

Optimize yet more. `-O3` turns on all optimizations specified by `-O2` and also turns on the `-finline-functions` and `-frename-registers` options.  

`-O0`

Do not optimize. This is the default.  

`-Os`

Optimize for size. `-Os` enables all `-O2` optimizations that do not typically increase code size. It also performs further optimizations designed to reduce code size.

`-Os` disables the following optimization flags:

          -falign-functions  -falign-jumps  -falign-loops 
          -falign-labels  -freorder-blocks  -fprefetch-loop-arrays
          

If you use multiple `-O` options, with or without level numbers, the last such option is the one that is effective.

Options of the form `-f`flag specify machine-independent flags. Most flags have both positive and negative forms; the negative form of `-ffoo` would be `-fno-foo`. In the table below, only one of the forms is listed--the one you typically will use. You can figure out the other form by either removing `no-` or adding it.

The following options control specific optimizations. They are either activated by `-O` options or are related to ones that are. You can use the following flags in the rare cases when "fine-tuning" of optimizations to be performed is desired.

`-fno-default-inline`

Do not make member functions inline by default merely because they are defined inside the class scope (C++ only). Otherwise, when you specify `-O`, member functions defined inside class scope are compiled inline by default; i.e., you don't need to add `inline` in front of the member function name.  

`-fno-defer-pop`

Always pop the arguments to each function call as soon as that function returns. For machines which must pop arguments after a function call, the compiler normally lets arguments accumulate on the stack for several function calls and pops them all at once.

Disabled at levels `-O`, `-O2`, `-O3`, `-Os`.  

`-fforce-mem`

Force memory operands to be copied into registers before doing arithmetic on them. This produces better code by making all memory references potential common subexpressions. When they are not common subexpressions, instruction combination should eliminate the separate register-load.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fforce-addr`

Force memory address constants to be copied into registers before doing arithmetic on them. This may produce better code just as `-fforce-mem` may.  

`-fomit-frame-pointer`

Don't keep the frame pointer in a register for functions that don't need one. This avoids the instructions to save, set up and restore frame pointers; it also makes an extra register available in many functions. **It also makes debugging impossible on some machines.**

On some machines, such as the VAX, this flag has no effect, because the standard calling sequence automatically handles the frame pointer and nothing is saved by pretending it doesn't exist. The machine-description macro `FRAME_POINTER_REQUIRED` controls whether a target machine supports this flag. See [Register Usage](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gccint/Registers.html#Registers).

Enabled at levels `-O`, `-O2`, `-O3`, `-Os`.  

`-foptimize-sibling-calls`

Optimize sibling and tail recursive calls.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fno-inline`

Don't pay attention to the `inline` keyword. Normally this option is used to keep the compiler from expanding any functions inline. Note that if you are not optimizing, no functions can be expanded inline.  

`-finline-functions`

Integrate all simple functions into their callers. The compiler heuristically decides which functions are simple enough to be worth integrating in this way.

If all calls to a given function are integrated, and the function is declared `static`, then the function is normally not output as assembler code in its own right.

Enabled at level `-O3`.  

`-finline-limit=`n

By default, gcc limits the size of functions that can be inlined. This flag allows the control of this limit for functions that are explicitly marked as inline (i.e., marked with the inline keyword or defined within the class definition in c++). n is the size of functions that can be inlined in number of pseudo instructions (not counting parameter handling). The default value of n is 600. Increasing this value can result in more inlined code at the cost of compilation time and memory consumption. Decreasing usually makes the compilation faster and less code will be inlined (which presumably means slower programs). This option is particularly useful for programs that use inlining heavily such as those based on recursive templates with C++.

Inlining is actually controlled by a number of parameters, which may be specified individually by using `--param` name`=`value. The `-finline-limit=`n option sets some of these parameters as follows:

  

`max-inline-insns`

is set to n.  

`max-inline-insns-single`

is set to n/2.  

`max-inline-insns-auto`

is set to n/2.  

`min-inline-insns`

is set to 130 or n/4, whichever is smaller.  

`max-inline-insns-rtl`

is set to n.

Using `-finline-limit=600` thus results in the default settings for these parameters. See below for a documentation of the individual parameters controlling inlining.

_Note:_ pseudo instruction represents, in this particular context, an abstract measurement of function's size. In no way, it represents a count of assembly instructions and as such its exact meaning might change from one release to an another.  

`-fkeep-inline-functions`

Even if all calls to a given function are integrated, and the function is declared `static`, nevertheless output a separate run-time callable version of the function. This switch does not affect `extern inline` functions.  

`-fkeep-static-consts`

Emit variables declared `static const` when optimization isn't turned on, even if the variables aren't referenced.

GCC enables this option by default. If you want to force the compiler to check if the variable was referenced, regardless of whether or not optimization is turned on, use the `-fno-keep-static-consts` option.  

`-fmerge-constants`

Attempt to merge identical constants (string constants and floating point constants) across compilation units.

This option is the default for optimized compilation if the assembler and linker support it. Use `-fno-merge-constants` to inhibit this behavior.

Enabled at levels `-O`, `-O2`, `-O3`, `-Os`.  

`-fmerge-all-constants`

Attempt to merge identical constants and identical variables.

This option implies `-fmerge-constants`. In addition to `-fmerge-constants` this considers e.g. even constant initialized arrays or initialized constant variables with integral or floating point types. Languages like C or C++ require each non-automatic variable to have distinct location, so using this option will result in non-conforming behavior.  

`-fno-branch-count-reg`

Do not use "decrement and branch" instructions on a count register, but instead generate a sequence of instructions that decrement a register, compare it against zero, then branch based upon the result. This option is only meaningful on architectures that support such instructions, which include x86, PowerPC, IA-64 and S/390.

The default is `-fbranch-count-reg`, enabled when `-fstrength-reduce` is enabled.  

`-fno-function-cse`

Do not put function addresses in registers; make each instruction that calls a constant function contain the function's address explicitly.

This option results in less efficient code, but some strange hacks that alter the assembler output may be confused by the optimizations performed when this option is not used.

The default is `-ffunction-cse`  

`-fno-zero-initialized-in-bss`

If the target supports a BSS section, GCC by default puts variables that are initialized to zero into BSS. This can save space in the resulting code.

This option turns off this behavior because some programs explicitly rely on variables going to the data section. E.g., so that the resulting executable can find the beginning of that section and/or make assumptions based on that.

The default is `-fzero-initialized-in-bss`.  

`-fstrength-reduce`

Perform the optimizations of loop strength reduction and elimination of iteration variables.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fthread-jumps`

Perform optimizations where we check to see if a jump branches to a location where another comparison subsumed by the first is found. If so, the first branch is redirected to either the destination of the second branch or a point immediately following it, depending on whether the condition is known to be true or false.

Enabled at levels `-O`, `-O2`, `-O3`, `-Os`.  

`-fcse-follow-jumps`

In common subexpression elimination, scan through jump instructions when the target of the jump is not reached by any other path. For example, when CSE encounters an `if` statement with an `else` clause, CSE will follow the jump when the condition tested is false.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fcse-skip-blocks`

This is similar to `-fcse-follow-jumps`, but causes CSE to follow jumps which conditionally skip over blocks. When CSE encounters a simple `if` statement with no else clause, `-fcse-skip-blocks` causes CSE to follow the jump around the body of the `if`.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-frerun-cse-after-loop`

Re-run common subexpression elimination after loop optimizations has been performed.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-frerun-loop-opt`

Run the loop optimizer twice.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fgcse`

Perform a global common subexpression elimination pass. This pass also performs global constant and copy propagation.

_Note:_ When compiling a program using computed gotos, a GCC extension, you may get better runtime performance if you disable the global common subexpression elimination pass by adding `-fno-gcse` to the command line.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fgcse-lm`

When `-fgcse-lm` is enabled, global common subexpression elimination will attempt to move loads which are only killed by stores into themselves. This allows a loop containing a load/store sequence to be changed to a load outside the loop, and a copy/store within the loop.

Enabled by default when gcse is enabled.  

`-fgcse-sm`

When `-fgcse-sm` is enabled, A store motion pass is run after global common subexpression elimination. This pass will attempt to move stores out of loops. When used in conjunction with `-fgcse-lm`, loops containing a load/store sequence can be changed to a load before the loop and a store after the loop.

Enabled by default when gcse is enabled.  

`-floop-optimize`

Perform loop optimizations: move constant expressions out of loops, simplify exit test conditions and optionally do strength-reduction and loop unrolling as well.

Enabled at levels `-O`, `-O2`, `-O3`, `-Os`.  

`-fcrossjumping`

Perform cross-jumping transformation. This transformation unifies equivalent code and save code size. The resulting code may or may not perform better than without cross-jumping.

Enabled at levels `-O`, `-O2`, `-O3`, `-Os`.  

`-fif-conversion`

Attempt to transform conditional jumps into branch-less equivalents. This include use of conditional moves, min, max, set flags and abs instructions, and some tricks doable by standard arithmetics. The use of conditional execution on chips where it is available is controlled by `if-conversion2`.

Enabled at levels `-O`, `-O2`, `-O3`, `-Os`.  

`-fif-conversion2`

Use conditional execution (where available) to transform conditional jumps into branch-less equivalents.

Enabled at levels `-O`, `-O2`, `-O3`, `-Os`.  

`-fdelete-null-pointer-checks`

Use global dataflow analysis to identify and eliminate useless checks for null pointers. The compiler assumes that dereferencing a null pointer would have halted the program. If a pointer is checked after it has already been dereferenced, it cannot be null.

In some environments, this assumption is not true, and programs can safely dereference null pointers. Use `-fno-delete-null-pointer-checks` to disable this optimization for programs which depend on that behavior.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fexpensive-optimizations`

Perform a number of minor optimizations that are relatively expensive.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-foptimize-register-move`

`-fregmove`

Attempt to reassign register numbers in move instructions and as operands of other simple instructions in order to maximize the amount of register tying. This is especially helpful on machines with two-operand instructions.

Note `-fregmove` and `-foptimize-register-move` are the same optimization.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fdelayed-branch`

If supported for the target machine, attempt to reorder instructions to exploit instruction slots available after delayed branch instructions.

Enabled at levels `-O`, `-O2`, `-O3`, `-Os`.  

`-fschedule-insns`

If supported for the target machine, attempt to reorder instructions to eliminate execution stalls due to required data being unavailable. This helps machines that have slow floating point or memory load instructions by allowing other instructions to be issued until the result of the load or floating point instruction is required.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fschedule-insns2`

Similar to `-fschedule-insns`, but requests an additional pass of instruction scheduling after register allocation has been done. This is especially useful on machines with a relatively small number of registers and where memory load instructions take more than one cycle.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fno-sched-interblock`

Don't schedule instructions across basic blocks. This is normally enabled by default when scheduling before register allocation, i.e. with `-fschedule-insns` or at `-O2` or higher.  

`-fno-sched-spec`

Don't allow speculative motion of non-load instructions. This is normally enabled by default when scheduling before register allocation, i.e. with `-fschedule-insns` or at `-O2` or higher.  

`-fsched-spec-load`

Allow speculative motion of some load instructions. This only makes sense when scheduling before register allocation, i.e. with `-fschedule-insns` or at `-O2` or higher.  

`-fsched-spec-load-dangerous`

Allow speculative motion of more load instructions. This only makes sense when scheduling before register allocation, i.e. with `-fschedule-insns` or at `-O2` or higher.  

`-fcaller-saves`

Enable values to be allocated in registers that will be clobbered by function calls, by emitting extra instructions to save and restore the registers around such calls. Such allocation is done only when it seems to result in better code than would otherwise be produced.

This option is always enabled by default on certain machines, usually those which have no call-preserved registers to use instead.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fmove-all-movables`

Forces all invariant computations in loops to be moved outside the loop.  

`-freduce-all-givs`

Forces all general-induction variables in loops to be strength-reduced.

_Note:_ When compiling programs written in Fortran, `-fmove-all-movables` and `-freduce-all-givs` are enabled by default when you use the optimizer.

These options may generate better or worse code; results are highly dependent on the structure of loops within the source code.

These two options are intended to be removed someday, once they have helped determine the efficacy of various approaches to improving loop optimizations.

Please let us ([gcc@gcc.gnu.org](mailto:gcc@gcc.gnu.org) and [fortran@gnu.org](mailto:fortran@gnu.org)) know how use of these options affects the performance of your production code. We're very interested in code that runs _slower_ when these options are _enabled_.  

`-fno-peephole`

`-fno-peephole2`

Disable any machine-specific peephole optimizations. The difference between `-fno-peephole` and `-fno-peephole2` is in how they are implemented in the compiler; some targets use one, some use the other, a few use both.

`-fpeephole` is enabled by default. `-fpeephole2` enabled at levels `-O2`, `-O3`, `-Os`.  

`-fbranch-probabilities`

  

`-fno-guess-branch-probability`

Do not guess branch probabilities using a randomized model.

Sometimes gcc will opt to use a randomized model to guess branch probabilities, when none are available from either profiling feedback (`-fprofile-arcs`) or `__builtin_expect`. This means that different runs of the compiler on the same program may produce different object code.

In a hard real-time system, people don't want different runs of the compiler to produce code that has different behavior; minimizing non-determinism is of paramount import. This switch allows users to reduce non-determinism, possibly at the expense of inferior optimization.

The default is `-fguess-branch-probability` at levels `-O`, `-O2`, `-O3`, `-Os`.  

`-freorder-blocks`

Reorder basic blocks in the compiled function in order to reduce number of taken branches and improve code locality.

Enabled at levels `-O2`, `-O3`.  

`-freorder-functions`

Reorder basic blocks in the compiled function in order to reduce number of taken branches and improve code locality. This is implemented by using special subsections `text.hot` for most frequently executed functions and `text.unlikely` for unlikely executed functions. Reordering is done by the linker so object file format must support named sections and linker must place them in a reasonable way.

Also profile feedback must be available in to make this option effective. See `-fprofile-arcs` for details.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-fstrict-aliasing`

Allows the compiler to assume the strictest aliasing rules applicable to the language being compiled. For C (and C++), this activates optimizations based on the type of expressions. In particular, an object of one type is assumed never to reside at the same address as an object of a different type, unless the types are almost the same. For example, an `unsigned int` can alias an `int`, but not a `void*` or a `double`. A character type may alias any other type.

Pay special attention to code like this:

          union a_union {
            int i;
            double d;
          };
          
          int f() {
            a_union t;
            t.d = 3.0;
            return t.i;
          }
          

The practice of reading from a different union member than the one most recently written to (called "type-punning") is common. Even with `-fstrict-aliasing`, type-punning is allowed, provided the memory is accessed through the union type. So, the code above will work as expected. However, this code might not:

          int f() {
            a_union t;
            int* ip;
            t.d = 3.0;
            ip = &t.i;
            return *ip;
          }
          

Every language that wishes to perform language-specific alias analysis should define a function that computes, given an `tree` node, an alias set for the node. Nodes in different alias sets are not allowed to alias. For an example, see the C front-end function `c_get_alias_set`.

Enabled at levels `-O2`, `-O3`, `-Os`.  

`-falign-functions`

`-falign-functions=`n

Align the start of functions to the next power-of-two greater than n, skipping up to n bytes. For instance, `-falign-functions=32` aligns functions to the next 32-byte boundary, but `-falign-functions=24` would align to the next 32-byte boundary only if this can be done by skipping 23 bytes or less.

`-fno-align-functions` and `-falign-functions=1` are equivalent and mean that functions will not be aligned.

Some assemblers only support this flag when n is a power of two; in that case, it is rounded up.

If n is not specified or is zero, use a machine-dependent default.

Enabled at levels `-O2`, `-O3`.  

`-falign-labels`

`-falign-labels=`n

Align all branch targets to a power-of-two boundary, skipping up to n bytes like `-falign-functions`. This option can easily make code slower, because it must insert dummy operations for when the branch target is reached in the usual flow of the code.

`-fno-align-labels` and `-falign-labels=1` are equivalent and mean that labels will not be aligned.

If `-falign-loops` or `-falign-jumps` are applicable and are greater than this value, then their values are used instead.

If n is not specified or is zero, use a machine-dependent default which is very likely to be `1`, meaning no alignment.

Enabled at levels `-O2`, `-O3`.  

`-falign-loops`

`-falign-loops=`n

Align loops to a power-of-two boundary, skipping up to n bytes like `-falign-functions`. The hope is that the loop will be executed many times, which will make up for any execution of the dummy operations.

`-fno-align-loops` and `-falign-loops=1` are equivalent and mean that loops will not be aligned.

If n is not specified or is zero, use a machine-dependent default.

Enabled at levels `-O2`, `-O3`.  

`-falign-jumps`

`-falign-jumps=`n

Align branch targets to a power-of-two boundary, for branch targets where the targets can only be reached by jumping, skipping up to n bytes like `-falign-functions`. In this case, no dummy operations need be executed.

`-fno-align-jumps` and `-falign-jumps=1` are equivalent and mean that loops will not be aligned.

If n is not specified or is zero, use a machine-dependent default.

Enabled at levels `-O2`, `-O3`.  

`-frename-registers`

Attempt to avoid false dependencies in scheduled code by making use of registers left over after register allocation. This optimization will most benefit processors with lots of registers. It can, however, make debugging impossible, since variables will no longer stay in a "home register".

Enabled at levels `-O3`.  

`-fno-cprop-registers`

After register allocation and post-register allocation instruction splitting, we perform a copy-propagation pass to try to reduce scheduling dependencies and occasionally eliminate the copy.

Disabled at levels `-O`, `-O2`, `-O3`, `-Os`.

The following options control compiler behavior regarding floating point arithmetic. These options trade off between speed and correctness. All must be specifically enabled.

`-ffloat-store`

Do not store floating point variables in registers, and inhibit other options that might change whether a floating point value is taken from a register or memory.

This option prevents undesirable excess precision on machines such as the 68000 where the floating registers (of the 68881) keep more precision than a `double` is supposed to have. Similarly for the x86 architecture. For most programs, the excess precision does only good, but a few programs rely on the precise definition of IEEE floating point. Use `-ffloat-store` for such programs, after modifying them to store all pertinent intermediate computations into variables.  

`-ffast-math`

Sets `-fno-math-errno`, `-funsafe-math-optimizations`,  
`-fno-trapping-math`, `-ffinite-math-only` and  
`-fno-signaling-nans`.

This option causes the preprocessor macro `__FAST_MATH__` to be defined.

This option should never be turned on by any `-O` option since it can result in incorrect output for programs which depend on an exact implementation of IEEE or ISO rules/specifications for math functions.  

`-fno-math-errno`

Do not set ERRNO after calling math functions that are executed with a single instruction, e.g., sqrt. A program that relies on IEEE exceptions for math error handling may want to use this flag for speed while maintaining IEEE arithmetic compatibility.

This option should never be turned on by any `-O` option since it can result in incorrect output for programs which depend on an exact implementation of IEEE or ISO rules/specifications for math functions.

The default is `-fmath-errno`.  

`-funsafe-math-optimizations`

Allow optimizations for floating-point arithmetic that (a) assume that arguments and results are valid and (b) may violate IEEE or ANSI standards. When used at link-time, it may include libraries or startup files that change the default FPU control word or other similar optimizations.

This option should never be turned on by any `-O` option since it can result in incorrect output for programs which depend on an exact implementation of IEEE or ISO rules/specifications for math functions.

The default is `-fno-unsafe-math-optimizations`.  

`-ffinite-math-only`

Allow optimizations for floating-point arithmetic that assume that arguments and results are not NaNs or +-Infs.

This option should never be turned on by any `-O` option since it can result in incorrect output for programs which depend on an exact implementation of IEEE or ISO rules/specifications.

The default is `-fno-finite-math-only`.  

`-fno-trapping-math`

Compile code assuming that floating-point operations cannot generate user-visible traps. These traps include division by zero, overflow, underflow, inexact result and invalid operation. This option implies `-fno-signaling-nans`. Setting this option may allow faster code if one relies on "non-stop" IEEE arithmetic, for example.

This option should never be turned on by any `-O` option since it can result in incorrect output for programs which depend on an exact implementation of IEEE or ISO rules/specifications for math functions.

The default is `-ftrapping-math`.  

`-fsignaling-nans`

Compile code assuming that IEEE signaling NaNs may generate user-visible traps during floating-point operations. Setting this option disables optimizations that may change the number of exceptions visible with signaling NaNs. This option implies `-ftrapping-math`.

This option causes the preprocessor macro `__SUPPORT_SNAN__` to be defined.

The default is `-fno-signaling-nans`.

This option is experimental and does not currently guarantee to disable all GCC optimizations that affect signaling NaN behavior.  

`-fsingle-precision-constant`

Treat floating point constant as single precision constant instead of implicitly converting it to double precision constant.

The following options control optimizations that may improve performance, but are not enabled by any `-O` options. This section includes experimental options that may produce broken code.

`-fbranch-probabilities`

After running a program compiled with `-fprofile-arcs` (see [Options for Debugging Your Program or `gcc`](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Debugging-Options.html#Debugging%20Options)), you can compile it a second time using `-fbranch-probabilities`, to improve optimizations based on the number of times each branch was taken. When the program compiled with `-fprofile-arcs` exits it saves arc execution counts to a file called sourcename`.da` for each source file The information in this data file is very dependent on the structure of the generated code, so you must use the same source code and the same optimization options for both compilations.

With `-fbranch-probabilities`, GCC puts a `REG_BR_PROB` note on each `JUMP_INSN` and `CALL_INSN`. These can be used to improve optimization. Currently, they are only used in one place: in `reorg.c`, instead of guessing which path a branch is mostly to take, the `REG_BR_PROB` values are used to exactly determine which path is taken more often.  

`-fnew-ra`

Use a graph coloring register allocator. Currently this option is meant for testing, so we are interested to hear about miscompilations with `-fnew-ra`.  

`-ftracer`

Perform tail duplication to enlarge superblock size. This transformation simplifies the control flow of the function allowing other optimizations to do better job.  

`-funroll-loops`

Unroll loops whose number of iterations can be determined at compile time or upon entry to the loop. `-funroll-loops` implies both `-fstrength-reduce` and `-frerun-cse-after-loop`. This option makes code larger, and may or may not make it run faster.  

`-funroll-all-loops`

Unroll all loops, even if their number of iterations is uncertain when the loop is entered. This usually makes programs run more slowly. `-funroll-all-loops` implies the same options as `-funroll-loops`,  

`-fprefetch-loop-arrays`

If supported by the target machine, generate instructions to prefetch memory to improve the performance of loops that access large arrays.

Disabled at level `-Os`.  

`-ffunction-sections`

`-fdata-sections`

Place each function or data item into its own section in the output file if the target supports arbitrary sections. The name of the function or the name of the data item determines the section's name in the output file.

Use these options on systems where the linker can perform optimizations to improve locality of reference in the instruction space. Most systems using the ELF object format and SPARC processors running Solaris 2 have linkers with such optimizations. AIX may have these optimizations in the future.

Only use these options when there are significant benefits from doing so. When you specify these options, the assembler and linker will create larger object and executable files and will also be slower. You will not be able to use `gprof` on all systems if you specify this option and you may have problems with debugging if you specify both this option and `-g`.  

`-fssa`

Perform optimizations in static single assignment form. Each function's flow graph is translated into SSA form, optimizations are performed, and the flow graph is translated back from SSA form. Users should not specify this option, since it is not yet ready for production use.  

`-fssa-ccp`

Perform Sparse Conditional Constant Propagation in SSA form. Requires `-fssa`. Like `-fssa`, this is an experimental feature.  

`-fssa-dce`

Perform aggressive dead-code elimination in SSA form. Requires `-fssa`. Like `-fssa`, this is an experimental feature.  

`--param` name`=`value

In some places, GCC uses various constants to control the amount of optimization that is done. For example, GCC will not inline functions that contain more that a certain number of instructions. You can control some of these constants on the command-line using the `--param` option.

In each case, the value is an integer. The allowable choices for name are given in the following table:

`max-crossjump-edges`

The maximum number of incoming edges to consider for crossjumping. The algorithm used by `-fcrossjumping` is O(N^2) in the number of edges incoming to each block. Increasing values mean more aggressive optimization, making the compile time increase with probably small improvement in executable size.  

`max-delay-slot-insn-search`

The maximum number of instructions to consider when looking for an instruction to fill a delay slot. If more than this arbitrary number of instructions is searched, the time savings from filling the delay slot will be minimal so stop searching. Increasing values mean more aggressive optimization, making the compile time increase with probably small improvement in executable run time.  

`max-delay-slot-live-search`

When trying to fill delay slots, the maximum number of instructions to consider when searching for a block with valid live register information. Increasing this arbitrarily chosen value means more aggressive optimization, increasing the compile time. This parameter should be removed when the delay slot code is rewritten to maintain the control-flow graph.  

`max-gcse-memory`

The approximate maximum amount of memory that will be allocated in order to perform the global common subexpression elimination optimization. If more memory than specified is required, the optimization will not be done.  

`max-gcse-passes`

The maximum number of passes of GCSE to run.  

`max-pending-list-length`

The maximum number of pending dependencies scheduling will allow before flushing the current state and starting over. Large functions with few branches or calls can create excessively large lists which needlessly consume memory and resources.  

`max-inline-insns-single`

Several parameters control the tree inliner used in gcc. This number sets the maximum number of instructions (counted in gcc's internal representation) in a single function that the tree inliner will consider for inlining. This only affects functions declared inline and methods implemented in a class declaration (C++). The default value is 300.  

`max-inline-insns-auto`

When you use `-finline-functions` (included in `-O3`), a lot of functions that would otherwise not be considered for inlining by the compiler will be investigated. To those functions, a different (more restrictive) limit compared to functions declared inline can be applied. The default value is 300.  

`max-inline-insns`

The tree inliner does decrease the allowable size for single functions to be inlined after we already inlined the number of instructions given here by repeated inlining. This number should be a factor of two or more larger than the single function limit. Higher numbers result in better runtime performance, but incur higher compile-time resource (CPU time, memory) requirements and result in larger binaries. Very high values are not advisable, as too large binaries may adversely affect runtime performance. The default value is 600.  

`max-inline-slope`

After exceeding the maximum number of inlined instructions by repeated inlining, a linear function is used to decrease the allowable size for single functions. The slope of that function is the negative reciprocal of the number specified here. The default value is 32.  

`min-inline-insns`

The repeated inlining is throttled more and more by the linear function after exceeding the limit. To avoid too much throttling, a minimum for this function is specified here to allow repeated inlining for very small functions even when a lot of repeated inlining already has been done. The default value is 130.  

`max-inline-insns-rtl`

For languages that use the RTL inliner (this happens at a later stage than tree inlining), you can set the maximum allowable size (counted in RTL instructions) for the RTL inliner with this parameter. The default value is 600.  

`max-unrolled-insns`

The maximum number of instructions that a loop should have if that loop is unrolled, and if the loop is unrolled, it determines how many times the loop code is unrolled.  

`hot-bb-count-fraction`

Select fraction of the maximal count of repetitions of basic block in program given basic block needs to have to be considered hot.  

`hot-bb-frequency-fraction`

Select fraction of the maximal frequency of executions of basic block in function given basic block needs to have to be considered hot  

`tracer-dynamic-coverage`

`tracer-dynamic-coverage-feedback`

This value is used to limit superblock formation once the given percentage of executed instructions is covered. This limits unnecessary code size expansion.

The `tracer-dynamic-coverage-feedback` is used only when profile feedback is available. The real profiles (as opposed to statically estimated ones) are much less balanced allowing the threshold to be larger value.  

`tracer-max-code-growth`

Stop tail duplication once code growth has reached given percentage. This is rather hokey argument, as most of the duplicates will be eliminated later in cross jumping, so it may be set to much higher values than is the desired code growth.  

`tracer-min-branch-ratio`

Stop reverse growth when the reverse probability of best edge is less than this threshold (in percent).  

`tracer-min-branch-ratio`

`tracer-min-branch-ratio-feedback`

Stop forward growth if the best edge do have probability lower than this threshold.

Similarly to `tracer-dynamic-coverage` two values are present, one for compilation for profile feedback and one for compilation without. The value for compilation with profile feedback needs to be more conservative (higher) in order to make tracer effective.  

`ggc-min-expand`

GCC uses a garbage collector to manage its own memory allocation. This parameter specifies the minimum percentage by which the garbage collector's heap should be allowed to expand between collections. Tuning this may improve compilation speed; it has no effect on code generation.

The default is 30% + 70% * (RAM/1GB) with an upper bound of 100% when RAM >= 1GB. If `getrlimit` is available, the notion of "RAM" is the smallest of actual RAM, RLIMIT_RSS, RLIMIT_DATA and RLIMIT_AS. If GCC is not able to calculate RAM on a particular platform, the lower bound of 30% is used. Setting this parameter and `ggc-min-heapsize` to zero causes a full collection to occur at every opportunity. This is extremely slow, but can be useful for debugging.  

`ggc-min-heapsize`

Minimum size of the garbage collector's heap before it begins bothering to collect garbage. The first collection occurs after the heap expands by `ggc-min-expand`% beyond `ggc-min-heapsize`. Again, tuning this may improve compilation speed, and has no effect on code generation.

The default is RAM/8, with a lower bound of 4096 (four megabytes) and an upper bound of 131072 (128 megabytes). If `getrlimit` is available, the notion of "RAM" is the smallest of actual RAM, RLIMIT_RSS, RLIMIT_DATA and RLIMIT_AS. If GCC is not able to calculate RAM on a particular platform, the lower bound is used. Setting this parameter very large effectively disables garbage collection. Setting this parameter and `ggc-min-expand` to zero causes a full collection to occur at every opportunity.