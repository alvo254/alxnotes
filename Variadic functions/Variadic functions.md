### A.2 Variadic Functions

ISO C defines a syntax for declaring a function to take a variable number or type of arguments. (Such functions are referred to as _varargs functions_ or _variadic functions_.) However, the language itself provides no mechanism for such functions to access their non-required arguments; instead, you use the variable arguments macros defined in stdarg.h.

This section describes how to declare variadic functions, how to write them, and how to call them properly.

**Compatibility Note:** Many older C dialects provide a similar, but incompatible, mechanism for defining functions with variable numbers of arguments, using varargs.h.

-   [Why Variadic Functions are Used](https://www.gnu.org/software/libc/manual/html_node/Why-Variadic.html)
-   [How Variadic Functions are Defined and Used](https://www.gnu.org/software/libc/manual/html_node/How-Variadic.html)
-   [Example of a Variadic Function](https://www.gnu.org/software/libc/manual/html_node/Variadic-Example.html)

[Variadic functions](https://www.geeksforgeeks.org/variadic-function-templates-c/) are [functions](https://www.geeksforgeeks.org/functions-in-c/) that can take a variable number of [arguments](https://www.geeksforgeeks.org/command-line-arguments-in-c-cpp/). In [C programming](https://www.geeksforgeeks.org/c/), a variadic function adds flexibility to the program. It takes one fixed argument and then any number of arguments can be passed. The variadic function consists of at least one fixed variable and then an ellipsis(…) as the last parameter.

**Syntax:**

int function_name(data_type variable_name, ...);

Values of the passed arguments can be accessed through the [header file](https://www.geeksforgeeks.org/header-files-in-c-cpp-and-its-uses/) named as:

#include <stdarg.h>


![[important.png]]