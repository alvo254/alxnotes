### Options Controlling C Dialect

The following options control the dialect of C (or languages derived from C, such as C++ and Objective-C) that the compiler accepts:

`-ansi`

In C mode, support all ISO C90 programs. In C++ mode, remove GNU extensions that conflict with ISO C++.

This turns off certain features of GCC that are incompatible with ISO C90 (when compiling C code), or of standard C++ (when compiling C++ code), such as the `asm` and `typeof` keywords, and predefined macros such as `unix` and `vax` that identify the type of system you are using. It also enables the undesirable and rarely used ISO trigraph feature. For the C compiler, it disables recognition of C++ style `//` comments as well as the `inline` keyword.

The alternate keywords `__asm__`, `__extension__`, `__inline__` and `__typeof__` continue to work despite `-ansi`. You would not want to use them in an ISO C program, of course, but it is useful to put them in header files that might be included in compilations done with `-ansi`. Alternate predefined macros such as `__unix__` and `__vax__` are also available, with or without `-ansi`.

The `-ansi` option does not cause non-ISO programs to be rejected gratuitously. For that, `-pedantic` is required in addition to `-ansi`. See [Warning Options](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Warning-Options.html#Warning%20Options).

The macro `__STRICT_ANSI__` is predefined when the `-ansi` option is used. Some header files may notice this macro and refrain from declaring certain functions or defining certain macros that the ISO standard doesn't call for; this is to avoid interfering with any programs that might use these names for other things.

Functions which would normally be built in but do not have semantics defined by ISO C (such as `alloca` and `ffs`) are not built-in functions with `-ansi` is used. See [Other built-in functions provided by GCC](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Other-Builtins.html#Other%20Builtins), for details of the functions affected.  

`-std=`

Determine the language standard. This option is currently only supported when compiling C or C++. A value for this option must be provided; possible values are

`c89`

`iso9899:1990`

ISO C90 (same as `-ansi`).  

`iso9899:199409`

ISO C90 as modified in amendment 1.  

`c99`

`c9x`

`iso9899:1999`

`iso9899:199x`

ISO C99. Note that this standard is not yet fully supported; see [http://gcc.gnu.org/gcc-3.3/c99status.html](http://gcc.gnu.org/gcc-3.3/c99status.html) for more information. The names `c9x` and `iso9899:199x` are deprecated.  

`gnu89`

Default, ISO C90 plus GNU extensions (including some C99 features).  

`gnu99`

  

`gnu9x`

ISO C99 plus GNU extensions. When ISO C99 is fully implemented in GCC, this will become the default. The name `gnu9x` is deprecated.  

`c++98`

The 1998 ISO C++ standard plus amendments.  

`gnu++98`

The same as `-std=c++98` plus GNU extensions. This is the default for C++ code.

Even when this option is not specified, you can still use some of the features of newer standards in so far as they do not conflict with previous C standards. For example, you may use `__restrict__` even when `-std=c99` is not specified.

The `-std` options specifying some version of ISO C have the same effects as `-ansi`, except that features that were not in ISO C90 but are in the specified version (for example, `//` comments and the `inline` keyword in ISO C99) are not disabled.

See [Language Standards Supported by GCC](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Standards.html#Standards), for details of these standard versions.  

`-aux-info` filename

Output to the given filename prototyped declarations for all functions declared and/or defined in a translation unit, including those in header files. This option is silently ignored in any language other than C.

Besides declarations, the file indicates, in comments, the origin of each declaration (source file and line), whether the declaration was implicit, prototyped or unprototyped (`I`, `N` for new or `O` for old, respectively, in the first character after the line number and the colon), and whether it came from a declaration or a definition (`C` or `F`, respectively, in the following character). In the case of function definitions, a K&R-style list of arguments followed by their declarations is also provided, inside comments, after the declaration.  

`-fno-asm`

Do not recognize `asm`, `inline` or `typeof` as a keyword, so that code can use these words as identifiers. You can use the keywords `__asm__`, `__inline__` and `__typeof__` instead. `-ansi` implies `-fno-asm`.

In C++, this switch only affects the `typeof` keyword, since `asm` and `inline` are standard keywords. You may want to use the `-fno-gnu-keywords` flag instead, which has the same effect. In C99 mode (`-std=c99` or `-std=gnu99`), this switch only affects the `asm` and `typeof` keywords, since `inline` is a standard keyword in ISO C99.  

`-fno-builtin`

`-fno-builtin-`function

Don't recognize built-in functions that do not begin with `__builtin_` as prefix. See [Other built-in functions provided by GCC](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Other-Builtins.html#Other%20Builtins), for details of the functions affected, including those which are not built-in functions when `-ansi` or `-std` options for strict ISO C conformance are used because they do not have an ISO standard meaning.

GCC normally generates special code to handle certain built-in functions more efficiently; for instance, calls to `alloca` may become single instructions that adjust the stack directly, and calls to `memcpy` may become inline copy loops. The resulting code is often both smaller and faster, but since the function calls no longer appear as such, you cannot set a breakpoint on those calls, nor can you change the behavior of the functions by linking with a different library.

With the `-fno-builtin-`function option only the built-in function function is disabled. function must not begin with `__builtin_`. If a function is named this is not built-in in this version of GCC, this option is ignored. There is no corresponding `-fbuiltin-`function option; if you wish to enable built-in functions selectively when using `-fno-builtin` or `-ffreestanding`, you may define macros such as:

          #define abs(n)          __builtin_abs ((n))
          #define strcpy(d, s)    __builtin_strcpy ((d), (s))
          

  

`-fhosted`

Assert that compilation takes place in a hosted environment. This implies `-fbuiltin`. A hosted environment is one in which the entire standard library is available, and in which `main` has a return type of `int`. Examples are nearly everything except a kernel. This is equivalent to `-fno-freestanding`.  

`-ffreestanding`

Assert that compilation takes place in a freestanding environment. This implies `-fno-builtin`. A freestanding environment is one in which the standard library may not exist, and program startup may not necessarily be at `main`. The most obvious example is an OS kernel. This is equivalent to `-fno-hosted`.

See [Language Standards Supported by GCC](https://gcc.gnu.org/onlinedocs/gcc-3.3.2/gcc/Standards.html#Standards), for details of freestanding and hosted environments.  

`-fms-extensions`

Accept some non-standard constructs used in Microsoft header files.  

`-trigraphs`

Support ISO C trigraphs. The `-ansi` option (and `-std` options for strict ISO C conformance) implies `-trigraphs`.  

`-no-integrated-cpp`

Performs a compilation in two passes: preprocessing and compiling. This option allows a user supplied "cc1", "cc1plus", or "cc1obj" via the `-B` option. The user supplied compilation step can then add in an additional preprocessing step after normal preprocessing but before compiling. The default is to use the integrated cpp (internal cpp)

The semantics of this option will change if "cc1", "cc1plus", and "cc1obj" are merged.  

`-traditional`

`-traditional-cpp`

Formerly, these options caused GCC to attempt to emulate a pre-standard C compiler. They are now only supported with the `-E` switch. The preprocessor continues to support a pre-standard mode. See the GNU CPP manual for details.  

`-fcond-mismatch`

Allow conditional expressions with mismatched types in the second and third arguments. The value of such an expression is void. This option is not supported for C++.  

`-funsigned-char`

Let the type `char` be unsigned, like `unsigned char`.

Each kind of machine has a default for what `char` should be. It is either like `unsigned char` by default or like `signed char` by default.

Ideally, a portable program should always use `signed char` or `unsigned char` when it depends on the signedness of an object. But many programs have been written to use plain `char` and expect it to be signed, or expect it to be unsigned, depending on the machines they were written for. This option, and its inverse, let you make such a program work with the opposite default.

The type `char` is always a distinct type from each of `signed char` or `unsigned char`, even though its behavior is always just like one of those two.  

`-fsigned-char`

Let the type `char` be signed, like `signed char`.

Note that this is equivalent to `-fno-unsigned-char`, which is the negative form of `-funsigned-char`. Likewise, the option `-fno-signed-char` is equivalent to `-funsigned-char`.  

`-fsigned-bitfields`

`-funsigned-bitfields`

`-fno-signed-bitfields`

`-fno-unsigned-bitfields`

These options control whether a bit-field is signed or unsigned, when the declaration does not use either `signed` or `unsigned`. By default, such a bit-field is signed, because this is consistent: the basic integer types such as `int` are signed types.  

`-fwritable-strings`

Store string constants in the writable data segment and don't uniquize them. This is for compatibility with old programs which assume they can write into string constants.

Writing into string constants is a very bad idea; "constants" should be constant.