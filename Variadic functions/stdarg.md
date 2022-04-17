**`stdarg.h`** is a header in the [C standard library](https://en.wikipedia.org/wiki/C_standard_library "C standard library") of the [C programming language](https://en.wikipedia.org/wiki/C_(programming_language) "C (programming language)") that allows functions to accept [an indefinite number of arguments](https://en.wikipedia.org/wiki/Variadic_function#Example_in_C "Variadic function").[[1]](https://en.wikipedia.org/wiki/Stdarg.h#cite_note-1) It provides facilities for stepping through a list of function arguments of unknown number and type. [C++](https://en.wikipedia.org/wiki/C%2B%2B "C++") provides this functionality in the header `cstdarg`.

The contents of `stdarg.h` are typically used in [variadic functions](https://en.wikipedia.org/wiki/Variadic_function "Variadic function"), though they may be used in other functions (for example, `[vprintf](https://en.wikipedia.org/wiki/Vprintf "Vprintf")`) called by variadic functions.

## Contents

-   [1Declaring variadic functions](https://en.wikipedia.org/wiki/Stdarg.h#Declaring_variadic_functions)
-   [2Defining variadic functions](https://en.wikipedia.org/wiki/Stdarg.h#Defining_variadic_functions)
-   [3stdarg.h types](https://en.wikipedia.org/wiki/Stdarg.h#stdarg.h_types)
-   [4stdarg.h macros](https://en.wikipedia.org/wiki/Stdarg.h#stdarg.h_macros)
-   [5Accessing the arguments](https://en.wikipedia.org/wiki/Stdarg.h#Accessing_the_arguments)
    -   [5.1Passing unnamed arguments to other calls](https://en.wikipedia.org/wiki/Stdarg.h#Passing_unnamed_arguments_to_other_calls)
-   [6Type safety](https://en.wikipedia.org/wiki/Stdarg.h#Type_safety)
-   [7Example](https://en.wikipedia.org/wiki/Stdarg.h#Example)
-   [8varargs.h](https://en.wikipedia.org/wiki/Stdarg.h#varargs.h)
-   [9References](https://en.wikipedia.org/wiki/Stdarg.h#References)

## Declaring variadic functions[[edit](https://en.wikipedia.org/w/index.php?title=Stdarg.h&action=edit&section=1 "Edit section: Declaring variadic functions")]

[Variadic functions](https://en.wikipedia.org/wiki/Variadic_functions "Variadic functions") are functions which may take a variable number of arguments and are declared with an [ellipsis](https://en.wikipedia.org/wiki/Ellipsis "Ellipsis") in place of the last parameter. An example of such a function is `[printf](https://en.wikipedia.org/wiki/Printf "Printf")`. A typical declaration is

int check(int a, double b, ...);

Variadic functions must have at least one named parameter, so, for instance,

char *wrong(...);

is not allowed in C. (In C++, such a declaration is permitted.) In C, a comma must precede the ellipsis; in C++, it is optional.

## Defining variadic functions[[edit](https://en.wikipedia.org/w/index.php?title=Stdarg.h&action=edit&section=2 "Edit section: Defining variadic functions")]

The same syntax is used in a definition:

long func(char, double, int, ...);

long func(char a, double b, int c, ...)
{
    /* ... */
}

An ellipsis may not appear in old-style function definitions.

## stdarg.h types[[edit](https://en.wikipedia.org/w/index.php?title=Stdarg.h&action=edit&section=3 "Edit section: stdarg.h types")]

Name

Description

Compatibility

`[va_list](http://en.cppreference.com/w/cpp/utility/variadic/va_list)`

type for iterating arguments

[C89](https://en.wikipedia.org/wiki/C89_(C_version) "C89 (C version)")

## stdarg.h macros[[edit](https://en.wikipedia.org/w/index.php?title=Stdarg.h&action=edit&section=4 "Edit section: stdarg.h macros")]

Name

Description

compatibility

`[va_start](http://en.cppreference.com/w/cpp/utility/variadic/va_start)`

Start iterating arguments with a `va_list`

C89

`[va_arg](http://en.cppreference.com/w/cpp/utility/variadic/va_arg)`

Retrieve an argument

C89

`[va_end](http://en.cppreference.com/w/cpp/utility/variadic/va_end)`

Free a `va_list`

C89

`[va_copy](http://en.cppreference.com/w/cpp/utility/variadic/va_copy)`

Copy contents of one `va_list` to another

[C99](https://en.wikipedia.org/wiki/C99 "C99")

## Accessing the arguments[[edit](https://en.wikipedia.org/w/index.php?title=Stdarg.h&action=edit&section=5 "Edit section: Accessing the arguments")]

To access the unnamed arguments, one must declare a variable of type `va_list` in the variadic function. The macro `va_start` is then called with two arguments: the first is the variable declared of the type `va_list`, the second is the name of the last named parameter of the function. After this, each invocation of the `va_arg` macro yields the next argument. The first argument to `va_arg` is the `va_list` and the second is the type of the next argument passed to the function. Finally, the `va_end` macro must be called on the `va_list` before the function returns. (It is not required to read in all the arguments.)

[C99](https://en.wikipedia.org/wiki/C99 "C99") provides an additional macro, `va_copy`, which can duplicate the state of a `va_list`. The macro invocation `va_copy(va2, va1)` copies `va1` into `va2`.

There is no mechanism defined for determining the number or types of the unnamed arguments passed to the function. The function is simply required to know or determine this somehow, the means of which vary. Common conventions include:

-   Use of a `[printf](https://en.wikipedia.org/wiki/Printf "Printf")` or `[scanf](https://en.wikipedia.org/wiki/Scanf "Scanf")`-like format string with embedded specifiers that indicate argument types.
-   A [sentinel value](https://en.wikipedia.org/wiki/Sentinel_value "Sentinel value") at the end of the variadic arguments.
-   A count argument indicating the number of variadic arguments.

### Passing unnamed arguments to other calls[[edit](https://en.wikipedia.org/w/index.php?title=Stdarg.h&action=edit&section=6 "Edit section: Passing unnamed arguments to other calls")]

Because the size of the unnamed argument list is generally unknown (the calling conventions employed by most compilers do not permit determining the size of the unnamed argument block pointed at by `va_list` inside the receiving function), there is also no reliable, generic way to forward the unnamed arguments into another variadic function. Even where determining the size of the argument list is possible by indirect means (for example, by parsing the format string of `fprintf()`), there is no portable way to pass the dynamically determined number of arguments into the inner variadic call, as the number and size of arguments passed into such calls must generally be known at compile time. To some extent, this restriction can be relaxed by employing [variadic macros](https://en.wikipedia.org/wiki/Variadic_macro "Variadic macro") instead of variadic functions. Additionally, most standard library procedures provide `v`-prefixed alternative versions which accept a _reference_ to the unnamed argument list (i.e. an initialized `va_list` variable) instead of the unnamed argument list itself. For example, `vfprintf()` is an alternate version of `fprintf()` expecting a `va_list` instead of the actual unnamed argument list. A user-defined variadic function can therefore initialize a `va_list` variable using `va_start` and pass it to an appropriate standard library function, in effect passing the unnamed argument list by reference instead of doing it by value. Because there is no reliable way to pass unnamed argument lists by value in C, providing variadic [API](https://en.wikipedia.org/wiki/Application_programming_interface "Application programming interface") functions without also providing equivalent functions accepting `va_list` instead is considered a bad programming practice.

## Type safety[[edit](https://en.wikipedia.org/w/index.php?title=Stdarg.h&action=edit&section=7 "Edit section: Type safety")]

Some C implementations provide C extensions that allow the compiler to check for the proper use of format strings and sentinels. Barring these extensions, the compiler usually cannot check whether the unnamed arguments passed are of the type the function expects, or convert them to the required type. Therefore, care should be taken to ensure correctness in this regard, since [undefined behavior](https://en.wikipedia.org/wiki/Undefined_behavior "Undefined behavior") results if the types do not match. For example, if the expected type is `int *`, then a null pointer should be passed as `(int *)NULL`. Writing just `NULL` would result in an argument of type either `int` or `void *`, neither of which is correct. Another consideration is the default argument [promotions](https://en.wikipedia.org/wiki/Type_conversion#Type_promotion_in_C-like_languages "Type conversion") applied to the unnamed arguments. A `float` will automatically be promoted to a `double`. Likewise, arguments of types narrower than an `int` will be promoted to `int` or `unsigned int`. The function receiving the unnamed arguments must expect the promoted type.

[GCC](https://en.wikipedia.org/wiki/GNU_Compiler_Collection "GNU Compiler Collection") has an extension that checks the passed arguments:

> **`format(archetype, string-index, first-to-check)`**
> 
> The format attribute specifies that a function takes `printf`, `scanf`, `strftime` or `strfmon` style arguments which should be type-checked against a format string. For example, the declaration:
> 
> extern int
> my_printf (void *my_object, const char *my_format, ...)
>       __attribute__ ((format (printf, 2, 3)));
> 
> causes the compiler to check the arguments in calls to `my_printf` for consistency with the `printf` style format string argument `my_format`.
> 
> — ["5.27 Extensions to the C Language Family - Declaring Attributes of Functions"](https://gcc.gnu.org/onlinedocs/gcc-4.3.2/gcc/Function-Attributes.html#Function-Attributes). Retrieved 2009-01-03.

## Example[[edit](https://en.wikipedia.org/w/index.php?title=Stdarg.h&action=edit&section=8 "Edit section: Example")]

#include <stdio.h>
#include <stdarg.h>

/* print all args one at a time until a negative argument is seen;
   all args are assumed to be of int type */
void printargs(int arg1, ...)
{
  va_list ap;
  int i;

  va_start(ap, arg1); 
  for (i = arg1; i >= 0; i = va_arg(ap, int))
    printf("%d ", i);
  va_end(ap);
  putchar('\n');
}

int main(void)
{
   printargs(5, 2, 14, 84, 97, 15, -1, 48, -1);
   printargs(84, 51, -1, 3);
   printargs(-1);
   printargs(1, -1);
   return 0;
}

This program yields the output:

5 2 14 84 97 15
84 51

1

To call other var args functions from within your function (such as sprintf) you need to use the var arg version of the function (vsprintf in this example):

void MyPrintf(const char *format, ...)
{
  va_list args;
  char buffer[BUFSIZ];

  va_start(args, format);
  vsnprintf(buffer, sizeof buffer, format, args);
  va_end(args);
  FlushFunnyStream(buffer);
}

## varargs.h[[edit](https://en.wikipedia.org/w/index.php?title=Stdarg.h&action=edit&section=9 "Edit section: varargs.h")]

Outdated versions of [POSIX](https://en.wikipedia.org/wiki/POSIX "POSIX") defined the legacy header `varargs.h`, which dates from before the standardization of C and provides functionality similar to `stdarg.h`. This header is part of neither ISO C nor POSIX. The file, as defined in the second version of the [Single UNIX Specification](https://en.wikipedia.org/wiki/Single_UNIX_Specification "Single UNIX Specification"), simply contains all of the functionality of C89 `stdarg.h`, with the exceptions that:

-   it cannot be used in standard C new-style definitions
-   the given argument may be omitted (standard C requires at least one argument)

The interface is also different. For `printargs` example, one would instead write:

#include <stdio.h>
#include <varargs.h>

/* There is no "void" type; use an implicit int return. */
printargs(arg1, va_alist)
  va_dcl /* no semicolon here! */
{
  va_list ap;
  int i;

  va_start(ap); 
  for (i = arg1; i >= 0; i = va_arg(ap, int))
    printf("%d ", i);
  va_end(ap);
  putchar('\n');
  return;
}

and is called the same way.

`varargs.h` requires old-style function definitions because of the way the implementation works.[[2]](https://en.wikipedia.org/wiki/Stdarg.h#cite_note-2) Conversely, it is not possible to mix old-style function definitions with `stdarg.h`.