Here is a summary of all the options, grouped by type. Explanations are in the following sections.

_Overall Options_

See [Options Controlling the Kind of Output](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Overall-Options.html#Overall%20Options).

          -c  -S  -E  -o file  -pipe  -pass-exit-codes  
          -x language  -v  -###  --help  --target-help  --version
          

  

_C Language Options_

See [Options Controlling C Dialect](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/C-Dialect-Options.html#C%20Dialect%20Options).

          -ansi  -std=standard  -aux-info filename 
          -fno-asm  -fno-builtin  -fno-builtin-function 
          -fhosted  -ffreestanding  -fms-extensions 
          -trigraphs  -no-integrated-cpp  -traditional  -traditional-cpp 
          -fallow-single-precision  -fcond-mismatch 
          -fsigned-bitfields  -fsigned-char 
          -funsigned-bitfields  -funsigned-char 
          -fwritable-strings
          

  

_C++ Language Options_

See [Options Controlling C++ Dialect](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/C---Dialect-Options.html#C++%20Dialect%20Options).

          -fabi-version=n  -fno-access-control  -fcheck-new 
          -fconserve-space  -fno-const-strings  -fdollars-in-identifiers 
          -fno-elide-constructors 
          -fno-enforce-eh-specs  -fexternal-templates 
          -falt-external-templates 
          -ffor-scope  -fno-for-scope  -fno-gnu-keywords 
          -fno-implicit-templates 
          -fno-implicit-inline-templates 
          -fno-implement-inlines  -fms-extensions 
          -fno-nonansi-builtins  -fno-operator-names 
          -fno-optional-diags  -fpermissive 
          -frepo  -fno-rtti  -fstats  -ftemplate-depth-n 
          -fuse-cxa-atexit  -fvtable-gc  -fno-weak  -nostdinc++ 
          -fno-default-inline  -Wabi  -Wctor-dtor-privacy 
          -Wnon-virtual-dtor  -Wreorder 
          -Weffc++  -Wno-deprecated 
          -Wno-non-template-friend  -Wold-style-cast 
          -Woverloaded-virtual  -Wno-pmf-conversions 
          -Wsign-promo  -Wsynth
          

  

_Objective-C Language Options_

See [Options Controlling Objective-C Dialect](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Objective-C-Dialect-Options.html#Objective-C%20Dialect%20Options).

          -fconstant-string-class=class-name 
          -fgnu-runtime  -fnext-runtime  -gen-decls 
          -Wno-protocol  -Wselector  -Wundeclared-selector
          

  

_Language Independent Options_

See [Options to Control Diagnostic Messages Formatting](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Language-Independent-Options.html#Language%20Independent%20Options).

          -fmessage-length=n 
          -fdiagnostics-show-location=[once|every-line]
          

  

_Warning Options_

See [Options to Request or Suppress Warnings](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Warning-Options.html#Warning%20Options).

          -fsyntax-only  -pedantic  -pedantic-errors 
          -w  -W  -Wall  -Waggregate-return 
          -Wcast-align  -Wcast-qual  -Wchar-subscripts  -Wcomment 
          -Wconversion  -Wno-deprecated-declarations 
          -Wdisabled-optimization  -Wno-div-by-zero  -Werror 
          -Wfloat-equal  -Wformat  -Wformat=2 
          -Wformat-nonliteral  -Wformat-security 
          -Wimplicit  -Wimplicit-int  
          -Wimplicit-function-declaration 
          -Werror-implicit-function-declaration 
          -Wimport  -Winline  -Wno-endif-labels 
          -Wlarger-than-len  -Wlong-long 
          -Wmain  -Wmissing-braces 
          -Wmissing-format-attribute  -Wmissing-noreturn 
          -Wno-multichar  -Wno-format-extra-args  -Wno-format-y2k 
          -Wno-import  -Wnonnull  -Wpacked  -Wpadded 
          -Wparentheses  -Wpointer-arith  -Wredundant-decls 
          -Wreturn-type  -Wsequence-point  -Wshadow 
          -Wsign-compare  -Wstrict-aliasing 
          -Wswitch  -Wswitch-default  -Wswitch-enum 
          -Wsystem-headers  -Wtrigraphs  -Wundef  -Wuninitialized 
          -Wunknown-pragmas  -Wunreachable-code 
          -Wunused  -Wunused-function  -Wunused-label  -Wunused-parameter 
          -Wunused-value  -Wunused-variable  -Wwrite-strings
          

  

_C-only Warning Options_

          -Wbad-function-cast  -Wmissing-declarations 
          -Wmissing-prototypes  -Wnested-externs 
          -Wstrict-prototypes  -Wtraditional
          

  

_Debugging Options_

See [Options for Debugging Your Program or GCC](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Debugging-Options.html#Debugging%20Options).

          -dletters  -dumpspecs  -dumpmachine  -dumpversion 
          -fdump-unnumbered  -fdump-translation-unit[-n] 
          -fdump-class-hierarchy[-n] 
          -fdump-tree-original[-n]  
          -fdump-tree-optimized[-n] 
          -fdump-tree-inlined[-n] 
          -feliminate-dwarf2-dups  -fmem-report 
          -fprofile-arcs  -frandom-seed=n 
          -fsched-verbose=n -ftest-coverage  -ftime-report 
          -g  -glevel  -gcoff  -gdwarf  -gdwarf-1  -gdwarf-1+  -gdwarf-2 
          -ggdb  -gstabs  -gstabs+  -gvms  -gxcoff  -gxcoff+ 
          -p  -pg  -print-file-name=library  -print-libgcc-file-name 
          -print-multi-directory  -print-multi-lib 
          -print-prog-name=program  -print-search-dirs  -Q 
          -save-temps  -time
          

  

_Optimization Options_

See [Options that Control Optimization](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Optimize-Options.html#Optimize%20Options).

          -falign-functions=n  -falign-jumps=n 
          -falign-labels=n  -falign-loops=n  
          -fbranch-probabilities  -fcaller-saves  -fcprop-registers 
          -fcse-follow-jumps  -fcse-skip-blocks  -fdata-sections 
          -fdelayed-branch  -fdelete-null-pointer-checks 
          -fexpensive-optimizations  -ffast-math  -ffloat-store 
          -fforce-addr  -fforce-mem  -ffunction-sections 
          -fgcse  -fgcse-lm  -fgcse-sm  -floop-optimize  -fcrossjumping 
          -fif-conversion  -fif-conversion2 
          -finline-functions  -finline-limit=n  -fkeep-inline-functions 
          -fkeep-static-consts  -fmerge-constants  -fmerge-all-constants 
          -fmove-all-movables  -fnew-ra  -fno-branch-count-reg 
          -fno-default-inline  -fno-defer-pop 
          -fno-function-cse  -fno-guess-branch-probability 
          -fno-inline  -fno-math-errno  -fno-peephole  -fno-peephole2 
          -funsafe-math-optimizations  -ffinite-math-only 
          -fno-trapping-math  -fno-zero-initialized-in-bss 
          -fomit-frame-pointer  -foptimize-register-move 
          -foptimize-sibling-calls  -fprefetch-loop-arrays 
          -freduce-all-givs  -fregmove  -frename-registers 
          -freorder-blocks  -freorder-functions 
          -frerun-cse-after-loop  -frerun-loop-opt 
          -fschedule-insns  -fschedule-insns2 
          -fno-sched-interblock  -fno-sched-spec  -fsched-spec-load 
          -fsched-spec-load-dangerous  -fsignaling-nans 
          -fsingle-precision-constant  -fssa  -fssa-ccp  -fssa-dce 
          -fstrength-reduce  -fstrict-aliasing  -ftracer  -fthread-jumps 
          -funroll-all-loops  -funroll-loops  
          --param name=value 
          -O  -O0  -O1  -O2  -O3  -Os
          

  

_Preprocessor Options_

See [Options Controlling the Preprocessor](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Preprocessor-Options.html#Preprocessor%20Options).

          -$  -Aquestion=answer 
          -A-question[=answer] 
          -C  -dD  -dI  -dM  -dN 
          -Dmacro[=defn]  -E  -H 
          -idirafter dir 
          -include file  -imacros file 
          -iprefix file  -iwithprefix dir 
          -iwithprefixbefore dir  -isystem dir 
          -M  -MM  -MF  -MG  -MP  -MQ  -MT  -nostdinc  -P  -remap 
          -trigraphs  -undef  -Umacro  -Wp,option
          

  

_Assembler Option_

See [Passing Options to the Assembler](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Assembler-Options.html#Assembler%20Options).

          -Wa,option
          

  

_Linker Options_

See [Options for Linking](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Link-Options.html#Link%20Options).

          object-file-name  -llibrary 
          -nostartfiles  -nodefaultlibs  -nostdlib 
          -s  -static  -static-libgcc  -shared  -shared-libgcc  -symbolic 
          -Wl,option  -Xlinker option 
          -u symbol
          

  

_Directory Options_

See [Options for Directory Search](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Directory-Options.html#Directory%20Options).

          -Bprefix  -Idir  -I-  -Ldir  -specs=file
          

  

_Target Options_

See [Target Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Target-Options.html#Target%20Options).

          -V version  -b machine
          

  

_Machine Dependent Options_

See [Hardware Models and Configurations](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Submodel-Options.html#Submodel%20Options).

_M680x0 Options_

          -m68000  -m68020  -m68020-40  -m68020-60  -m68030  -m68040 
          -m68060  -mcpu32  -m5200  -m68881  -mbitfield  -mc68000  -mc68020   
          -mfpa  -mnobitfield  -mrtd  -mshort  -msoft-float  -mpcrel 
          -malign-int  -mstrict-align
          

_M68hc1x Options_

          -m6811  -m6812  -m68hc11  -m68hc12  -m68hcs12 
          -mauto-incdec  -minmax  -mlong-calls  -mshort 
          -msoft-reg-count=count
          

_VAX Options_

          -mg  -mgnu  -munix
          

_SPARC Options_

          -mcpu=cpu-type 
          -mtune=cpu-type 
          -mcmodel=code-model 
          -m32  -m64 
          -mapp-regs  -mbroken-saverestore  -mcypress 
          -mfaster-structs  -mflat 
          -mfpu  -mhard-float  -mhard-quad-float 
          -mimpure-text  -mlittle-endian  -mlive-g0  -mno-app-regs 
          -mno-faster-structs  -mno-flat  -mno-fpu 
          -mno-impure-text  -mno-stack-bias  -mno-unaligned-doubles 
          -msoft-float  -msoft-quad-float  -msparclite  -mstack-bias 
          -msupersparc  -munaligned-doubles  -mv8
          

_ARM Options_

          -mapcs-frame  -mno-apcs-frame 
          -mapcs-26  -mapcs-32 
          -mapcs-stack-check  -mno-apcs-stack-check 
          -mapcs-float  -mno-apcs-float 
          -mapcs-reentrant  -mno-apcs-reentrant 
          -msched-prolog  -mno-sched-prolog 
          -mlittle-endian  -mbig-endian  -mwords-little-endian 
          -malignment-traps  -mno-alignment-traps 
          -msoft-float  -mhard-float  -mfpe 
          -mthumb-interwork  -mno-thumb-interwork 
          -mcpu=name  -march=name  -mfpe=name  
          -mstructure-size-boundary=n 
          -mabort-on-noreturn 
          -mlong-calls  -mno-long-calls 
          -msingle-pic-base  -mno-single-pic-base 
          -mpic-register=reg 
          -mnop-fun-dllimport 
          -mpoke-function-name 
          -mthumb  -marm 
          -mtpcs-frame  -mtpcs-leaf-frame 
          -mcaller-super-interworking  -mcallee-super-interworking
          

_MN10200 Options_

          -mrelax
          

_MN10300 Options_

          -mmult-bug  -mno-mult-bug 
          -mam33  -mno-am33 
          -mno-crt0  -mrelax
          

_M32R/D Options_

          -m32rx  -m32r  -mcode-model=model-type 
          -msdata=sdata-type  -G num
          

_M88K Options_

          -m88000  -m88100  -m88110  -mbig-pic 
          -mcheck-zero-division  -mhandle-large-shift 
          -midentify-revision  -mno-check-zero-division 
          -mno-ocs-debug-info  -mno-ocs-frame-position 
          -mno-optimize-arg-area  -mno-serialize-volatile 
          -mno-underscores  -mocs-debug-info 
          -mocs-frame-position  -moptimize-arg-area 
          -mserialize-volatile  -mshort-data-num  -msvr3 
          -msvr4  -mtrap-large-shift  -muse-div-instruction 
          -mversion-03.00  -mwarn-passed-structs
          

_RS/6000 and PowerPC Options_

          -mcpu=cpu-type 
          -mtune=cpu-type 
          -mpower  -mno-power  -mpower2  -mno-power2 
          -mpowerpc  -mpowerpc64  -mno-powerpc 
          -maltivec  -mno-altivec 
          -mpowerpc-gpopt  -mno-powerpc-gpopt 
          -mpowerpc-gfxopt  -mno-powerpc-gfxopt 
          -mnew-mnemonics  -mold-mnemonics 
          -mfull-toc   -mminimal-toc  -mno-fp-in-toc  -mno-sum-in-toc 
          -m64  -m32  -mxl-call  -mno-xl-call  -mpe 
          -msoft-float  -mhard-float  -mmultiple  -mno-multiple 
          -mstring  -mno-string  -mupdate  -mno-update 
          -mfused-madd  -mno-fused-madd  -mbit-align  -mno-bit-align 
          -mstrict-align  -mno-strict-align  -mrelocatable 
          -mno-relocatable  -mrelocatable-lib  -mno-relocatable-lib 
          -mtoc  -mno-toc  -mlittle  -mlittle-endian  -mbig  -mbig-endian 
          -mcall-aix  -mcall-sysv  -mcall-netbsd 
          -maix-struct-return  -msvr4-struct-return 
          -mabi=altivec  -mabi=no-altivec 
          -mabi=spe  -mabi=no-spe 
          -misel=yes  -misel=no 
          -mprototype  -mno-prototype 
          -msim  -mmvme  -mads  -myellowknife  -memb  -msdata 
          -msdata=opt  -mvxworks  -mwindiss  -G num  -pthread
          

_Darwin Options_

          -all_load -allowable_client -arch -arch_errors_fatal 
          -arch_only -bind_at_load -bundle -bundle_loader 
          -client_name -compatibility_version -current_version 
          -dependency-file -dylib_file -dylinker_install_name 
          -dynamic -dynamiclib -exported_symbols_list 
          -filelist -flat_namespace -force_cpusubtype_ALL 
          -force_flat_namespace -headerpad_max_install_names 
          -image_base -init -install_name -keep_private_externs 
          -multi_module -multiply_defined -multiply_defined_unused 
          -noall_load -nomultidefs -noprebind -noseglinkedit 
          -pagezero_size -prebind -prebind_all_twolevel_modules 
          -private_bundle -read_only_relocs -sectalign 
          -sectobjectsymbols -whyload -seg1addr 
          -sectcreate -sectobjectsymbols -sectorder 
          -seg_addr_table -seg_addr_table_filename -seglinkedit 
          -segprot -segs_read_only_addr -segs_read_write_addr 
          -single_module -static -sub_library -sub_umbrella 
          -twolevel_namespace -umbrella -undefined 
          -unexported_symbols_list -weak_reference_mismatches -whatsloaded
          

_RT Options_

          -mcall-lib-mul  -mfp-arg-in-fpregs  -mfp-arg-in-gregs 
          -mfull-fp-blocks  -mhc-struct-return  -min-line-mul 
          -mminimum-fp-blocks  -mnohc-struct-return
          

_MIPS Options_

          -mabicalls  -march=cpu-type  -mtune=cpu=type 
          -mcpu=cpu-type  -membedded-data  -muninit-const-in-rodata 
          -membedded-pic  -mfp32  -mfp64  -mfused-madd  -mno-fused-madd 
          -mgas  -mgp32  -mgp64 
          -mgpopt  -mhalf-pic  -mhard-float  -mint64  -mips1 
          -mips2  -mips3  -mips4  -mlong64  -mlong32  -mlong-calls  -mmemcpy 
          -mmips-as  -mmips-tfile  -mno-abicalls 
          -mno-embedded-data  -mno-uninit-const-in-rodata 
          -mno-embedded-pic  -mno-gpopt  -mno-long-calls 
          -mno-memcpy  -mno-mips-tfile  -mno-rnames  -mno-stats 
          -mrnames  -msoft-float 
          -m4650  -msingle-float  -mmad 
          -mstats  -EL  -EB  -G num  -nocpp 
          -mabi=32  -mabi=n32  -mabi=64  -mabi=eabi 
          -mfix7000  -mno-crt0  -mflush-func=func  -mno-flush-func 
          -mbranch-likely  -mno-branch-likely
          

_i386 and x86-64 Options_

          -mcpu=cpu-type  -march=cpu-type  
          -mfpmath=unit  -masm=dialect  -mno-fancy-math-387 
          -mno-fp-ret-in-387  -msoft-float  -msvr3-shlib 
          -mno-wide-multiply  -mrtd  -malign-double 
          -mpreferred-stack-boundary=num 
          -mmmx  -msse  -msse2  -m3dnow 
          -mthreads  -mno-align-stringops  -minline-all-stringops 
          -mpush-args  -maccumulate-outgoing-args  -m128bit-long-double 
          -m96bit-long-double  -mregparm=num  -momit-leaf-frame-pointer 
          -mno-red-zone
          -mcmodel=code-model 
          -m32  -m64
          

_HPPA Options_

          -march=architecture-type 
          -mbig-switch  -mdisable-fpregs  -mdisable-indexing 
          -mfast-indirect-calls  -mgas  -mgnu-ld  -mhp-ld 
          -mjump-in-delay  -mlinker-opt  -mlong-calls 
          -mlong-load-store  -mno-big-switch  -mno-disable-fpregs 
          -mno-disable-indexing  -mno-fast-indirect-calls  -mno-gas 
          -mno-jump-in-delay  -mno-long-load-store 
          -mno-portable-runtime  -mno-soft-float 
          -mno-space-regs  -msoft-float  -mpa-risc-1-0 
          -mpa-risc-1-1  -mpa-risc-2-0  -mportable-runtime 
          -mschedule=cpu-type  -mspace-regs  -msio  -mwsio 
          -nolibdld  -static  -threads
          

_Intel 960 Options_

          -mcpu-type  -masm-compat  -mclean-linkage 
          -mcode-align  -mcomplex-addr  -mleaf-procedures 
          -mic-compat  -mic2.0-compat  -mic3.0-compat 
          -mintel-asm  -mno-clean-linkage  -mno-code-align 
          -mno-complex-addr  -mno-leaf-procedures 
          -mno-old-align  -mno-strict-align  -mno-tail-call 
          -mnumerics  -mold-align  -msoft-float  -mstrict-align 
          -mtail-call
          

_DEC Alpha Options_

          -mno-fp-regs  -msoft-float  -malpha-as  -mgas 
          -mieee  -mieee-with-inexact  -mieee-conformant 
          -mfp-trap-mode=mode  -mfp-rounding-mode=mode 
          -mtrap-precision=mode  -mbuild-constants 
          -mcpu=cpu-type  -mtune=cpu-type 
          -mbwx  -mmax  -mfix  -mcix 
          -mfloat-vax  -mfloat-ieee 
          -mexplicit-relocs  -msmall-data  -mlarge-data 
          -mmemory-latency=time
          

_DEC Alpha/VMS Options_

          -mvms-return-codes
          

_H8/300 Options_

          -mrelax  -mh  -ms  -mn  -mint32  -malign-300
          

_SH Options_

          -m1  -m2  -m3  -m3e 
          -m4-nofpu  -m4-single-only  -m4-single  -m4 
          -m5-64media  -m5-64media-nofpu 
          -m5-32media  -m5-32media-nofpu 
          -m5-compact  -m5-compact-nofpu 
          -mb  -ml  -mdalign  -mrelax 
          -mbigtable  -mfmovd  -mhitachi  -mnomacsave 
          -mieee  -misize  -mpadstruct  -mspace 
          -mprefergot  -musermode
          

_System V Options_

          -Qy  -Qn  -YP,paths  -Ym,dir
          

_ARC Options_

          -EB  -EL 
          -mmangle-cpu  -mcpu=cpu  -mtext=text-section 
          -mdata=data-section  -mrodata=readonly-data-section
          

_TMS320C3x/C4x Options_

          -mcpu=cpu  -mbig  -msmall  -mregparm  -mmemparm 
          -mfast-fix  -mmpyi  -mbk  -mti  -mdp-isr-reload 
          -mrpts=count  -mrptb  -mdb  -mloop-unsigned 
          -mparallel-insns  -mparallel-mpy  -mpreserve-float
          

_V850 Options_

          -mlong-calls  -mno-long-calls  -mep  -mno-ep 
          -mprolog-function  -mno-prolog-function  -mspace 
          -mtda=n  -msda=n  -mzda=n 
          -mapp-regs  -mno-app-regs 
          -mdisable-callt  -mno-disable-callt 
          -mv850e 
          -mv850  -mbig-switch
          

_NS32K Options_

          -m32032  -m32332  -m32532  -m32081  -m32381 
          -mmult-add  -mnomult-add  -msoft-float  -mrtd  -mnortd 
          -mregparam  -mnoregparam  -msb  -mnosb 
          -mbitfield  -mnobitfield  -mhimem  -mnohimem
          

_AVR Options_

          -mmcu=mcu  -msize  -minit-stack=n  -mno-interrupts 
          -mcall-prologues  -mno-tablejump  -mtiny-stack
          

_MCore Options_

          -mhardlit  -mno-hardlit  -mdiv  -mno-div  -mrelax-immediates 
          -mno-relax-immediates  -mwide-bitfields  -mno-wide-bitfields 
          -m4byte-functions  -mno-4byte-functions  -mcallgraph-data 
          -mno-callgraph-data  -mslow-bytes  -mno-slow-bytes  -mno-lsim 
          -mlittle-endian  -mbig-endian  -m210  -m340  -mstack-increment
          

_MMIX Options_

          -mlibfuncs  -mno-libfuncs  -mepsilon  -mno-epsilon  -mabi=gnu 
          -mabi=mmixware  -mzero-extend  -mknuthdiv  -mtoplevel-symbols 
          -melf  -mbranch-predict  -mno-branch-predict  -mbase-addresses 
          -mno-base-addresses  -msingle-exit  -mno-single-exit
          

_IA-64 Options_

          -mbig-endian  -mlittle-endian  -mgnu-as  -mgnu-ld  -mno-pic 
          -mvolatile-asm-stop  -mb-step  -mregister-names  -mno-sdata 
          -mconstant-gp  -mauto-pic  -minline-float-divide-min-latency 
          -minline-float-divide-max-throughput 
          -minline-int-divide-min-latency 
          -minline-int-divide-max-throughput  -mno-dwarf2-asm 
          -mfixed-range=register-range
          

_D30V Options_

          -mextmem  -mextmemory  -monchip  -mno-asm-optimize 
          -masm-optimize  -mbranch-cost=n  -mcond-exec=n
          

_S/390 and zSeries Options_

          -mhard-float  -msoft-float  -mbackchain  -mno-backchain 
          -msmall-exec  -mno-small-exec  -mmvcle  -mno-mvcle 
          -m64  -m31  -mdebug  -mno-debug
          

_CRIS Options_

          -mcpu=cpu  -march=cpu  -mtune=cpu 
          -mmax-stack-frame=n  -melinux-stacksize=n 
          -metrax4  -metrax100  -mpdebug  -mcc-init  -mno-side-effects 
          -mstack-align  -mdata-align  -mconst-align 
          -m32-bit  -m16-bit  -m8-bit  -mno-prologue-epilogue  -mno-gotplt 
          -melf  -maout  -melinux  -mlinux  -sim  -sim2
          

_PDP-11 Options_

          -mfpu  -msoft-float  -mac0  -mno-ac0  -m40  -m45  -m10 
          -mbcopy  -mbcopy-builtin  -mint32  -mno-int16 
          -mint16  -mno-int32  -mfloat32  -mno-float64 
          -mfloat64  -mno-float32  -mabshi  -mno-abshi 
          -mbranch-expensive  -mbranch-cheap 
          -msplit  -mno-split  -munix-asm  -mdec-asm
          

_Xstormy16 Options_

          -msim
          

_Xtensa Options_

          -mbig-endian  -mlittle-endian 
          -mdensity  -mno-density 
          -mmac16  -mno-mac16 
          -mmul16  -mno-mul16 
          -mmul32  -mno-mul32 
          -mnsa  -mno-nsa 
          -mminmax  -mno-minmax 
          -msext  -mno-sext 
          -mbooleans  -mno-booleans 
          -mhard-float  -msoft-float 
          -mfused-madd  -mno-fused-madd 
          -mserialize-volatile  -mno-serialize-volatile 
          -mtext-section-literals  -mno-text-section-literals 
          -mtarget-align  -mno-target-align 
          -mlongcalls  -mno-longcalls
          

_FRV Options_

          -mgpr-32  -mgpr-64  -mfpr-32  -mfpr-64 
          -mhard-float  -msoft-float  -malloc-cc  -mfixed-cc 
          -mdword  -mno-dword  -mdouble  -mno-double 
          -mmedia  -mno-media  -mmuladd  -mno-muladd  -mlibrary-pic 
          -macc-4  -macc-8  -mpack  -mno-pack  -mno-eflags 
          -mcond-move  -mno-cond-move -mscc  -mno-scc  
          -mcond-exec  -mno-cond-exec  -mvliw-branch  -mno-vliw-branch 
          -mmulti-cond-exec  -mno-multi-cond-exec  -mnested-cond-exec 
          -mno-nested-cond-exec  -mtomcat-stats 
          -mcpu=cpu
          

  

_Code Generation Options_

See [Options for Code Generation Conventions](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Code-Gen-Options.html#Code%20Gen%20Options).

          -fcall-saved-reg  -fcall-used-reg 
          -ffixed-reg  -fexceptions 
          -fnon-call-exceptions  -funwind-tables 
          -fasynchronous-unwind-tables 
          -finhibit-size-directive  -finstrument-functions 
          -fno-common  -fno-ident  -fno-gnu-linker 
          -fpcc-struct-return  -fpic  -fPIC 
          -freg-struct-return  -fshared-data  -fshort-enums 
          -fshort-double  -fshort-wchar  -fvolatile 
          -fvolatile-global  -fvolatile-static 
          -fverbose-asm  -fpack-struct  -fstack-check 
          -fstack-limit-register=reg  -fstack-limit-symbol=sym 
          -fargument-alias  -fargument-noalias 
          -fargument-noalias-global  -fleading-underscore 
          -ftls-model=model 
          -ftrapv  -fbounds-check