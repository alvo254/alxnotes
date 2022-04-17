From Wikipedia, the free encyclopedia

[Jump to navigation](https://en.wikipedia.org/wiki/Include_guard#mw-head) [Jump to search](https://en.wikipedia.org/wiki/Include_guard#searchInput)

The correct title of this article is **#include guard**. The omission of the [#](https://en.wikipedia.org/wiki/Number_sign "Number sign") is due to [technical restrictions](https://en.wikipedia.org/wiki/Wikipedia:Naming_conventions_(technical_restrictions) "Wikipedia:Naming conventions (technical restrictions)").

![](https://upload.wikimedia.org/wikipedia/en/thumb/f/f2/Edit-clear.svg/40px-Edit-clear.svg.png)

This section **may be too technical for most readers to understand**. Please [help improve it](https://en.wikipedia.org/w/index.php?title=Include_guard&action=edit) to [make it understandable to non-experts](https://en.wikipedia.org/wiki/Wikipedia:Make_technical_articles_understandable "Wikipedia:Make technical articles understandable"), without removing the technical details. _(September 2018)_ _([Learn how and when to remove this template message](https://en.wikipedia.org/wiki/Help:Maintenance_template_removal "Help:Maintenance template removal"))_

In the [C](https://en.wikipedia.org/wiki/C_(programming_language) "C (programming language)") and [C++](https://en.wikipedia.org/wiki/C%2B%2B "C++") programming languages, an **#include guard**, sometimes called a **macro guard**, **header guard** or **file guard**, is a particular construct used to avoid the problem of _double inclusion_ when dealing with the [include directive](https://en.wikipedia.org/wiki/Include_directive "Include directive").

The [C preprocessor](https://en.wikipedia.org/wiki/C_preprocessor "C preprocessor") processes [directives](https://en.wikipedia.org/wiki/Preprocessor_directive "Preprocessor directive") of the form `#include <file>` in a [source file](https://en.wikipedia.org/wiki/Source_file "Source file") by locating the associated `file` on [disk](https://en.wikipedia.org/wiki/File_system "File system") and [transcluding](https://en.wikipedia.org/wiki/Transclusion "Transclusion") ("including") its contents into a copy of the source file known as the [translation unit](https://en.wikipedia.org/wiki/Translation_unit_(programming) "Translation unit (programming)"), replacing the include directive in the process. The files included in this regard are generally [header files](https://en.wikipedia.org/wiki/Header_file "Header file"), which typically contain [declarations](https://en.wikipedia.org/wiki/Declaration_(computer_programming) "Declaration (computer programming)") of [functions](https://en.wikipedia.org/wiki/Function_(computer_programming) "Function (computer programming)") and [classes](https://en.wikipedia.org/wiki/Class_(computer_programming) "Class (computer programming)") or [structs](https://en.wikipedia.org/wiki/Struct "Struct"). If certain C or C++ language constructs [are defined twice](https://en.wikipedia.org/wiki/One_Definition_Rule "One Definition Rule"), the resulting translation unit [is invalid](https://en.wikipedia.org/wiki/Compilation_error "Compilation error"). #include guards prevent this erroneous construct from arising by the double inclusion mechanism.

The addition of #include guards to a header file is one way to make that file [idempotent](https://en.wikipedia.org/wiki/Idempotent "Idempotent"). Another construct to combat _double inclusion_ is [#pragma once](https://en.wikipedia.org/wiki/Pragma_once "Pragma once"), which is non-standard but nearly universally supported among C and C++ [compilers](https://en.wikipedia.org/wiki/List_of_compilers "List of compilers").

## Contents

-   [1 Double inclusion](https://en.wikipedia.org/wiki/Include_guard#Double_inclusion)
    -   [1.1 Example](https://en.wikipedia.org/wiki/Include_guard#Example)
        -   [1.1.1 File "grandparent.h"](https://en.wikipedia.org/wiki/Include_guard#File_"grandparent.h")
        -   [1.1.2 File "parent.h"](https://en.wikipedia.org/wiki/Include_guard#File_"parent.h")
        -   [1.1.3 File "child.c"](https://en.wikipedia.org/wiki/Include_guard#File_"child.c")
        -   [1.1.4 Result](https://en.wikipedia.org/wiki/Include_guard#Result)
-   [2 Use of #include guards](https://en.wikipedia.org/wiki/Include_guard#Use_of_#include_guards)
    -   [2.1 Example](https://en.wikipedia.org/wiki/Include_guard#Example_2)
        -   [2.1.1 File "grandparent.h"](https://en.wikipedia.org/wiki/Include_guard#File_"grandparent.h"_2)
        -   [2.1.2 File "parent.h"](https://en.wikipedia.org/wiki/Include_guard#File_"parent.h"_2)
        -   [2.1.3 File "child.c"](https://en.wikipedia.org/wiki/Include_guard#File_"child.c"_2)
        -   [2.1.4 Result](https://en.wikipedia.org/wiki/Include_guard#Result_2)
    -   [2.2 Discussion](https://en.wikipedia.org/wiki/Include_guard#Discussion)
-   [3 Difficulties](https://en.wikipedia.org/wiki/Include_guard#Difficulties)
-   [4 Other languages](https://en.wikipedia.org/wiki/Include_guard#Other_languages)
-   [5 See also](https://en.wikipedia.org/wiki/Include_guard#See_also)
-   [6 References](https://en.wikipedia.org/wiki/Include_guard#References)
-   [7 External links](https://en.wikipedia.org/wiki/Include_guard#External_links)

## Double inclusion

### Example

The following C code demonstrates a real problem that can arise if #include guards are missing:

#### File "grandparent.h"

struct foo {
 int member;
};

#### File "parent.h"

#include "grandparent.h"

#### File "child.c"

#include "grandparent.h"
#include "parent.h"

#### Result

struct foo {
 int member;
};
struct foo {
 int member;
};

Here, the file "child.c" has indirectly included two copies of the text in the [header file](https://en.wikipedia.org/wiki/Header_file "Header file") "grandparent.h". This causes a [compilation error](https://en.wikipedia.org/wiki/Compilation_error "Compilation error"), since the structure type `foo` will thus be defined twice. In C++, this would be called a violation of the [one definition rule](https://en.wikipedia.org/wiki/One_Definition_Rule "One Definition Rule").

## Use of #include guards

### Example

In this section, the same code is used with the addition of #include guards. The [C preprocessor](https://en.wikipedia.org/wiki/C_preprocessor "C preprocessor") preprocesses the header files, including and further preprocessing them [recursively](https://en.wikipedia.org/wiki/Recursion_(computer_science) "Recursion (computer science)"). This will result in a correct source file, as we will see.

#### File "grandparent.h"

#ifndef GRANDPARENT_H
#define GRANDPARENT_H

struct foo {
 int member;
};

#endif /* GRANDPARENT_H */

#### File "parent.h"

#include "grandparent.h"

#### File "child.c"

#include "grandparent.h"
#include "parent.h"

#### Result

struct foo {
 int member;
};

Here, the first inclusion of "grandparent.h" has the macro `GRANDPARENT_H` defined. When "child.c" includes "grandparent.h" at the second time, as the `#ifndef` test returns false, the preprocessor skips down to the `#endif`, thus avoiding the second definition of `struct foo`. The program compiles correctly.

### Discussion

Different [naming conventions](https://en.wikipedia.org/wiki/Naming_conventions_(programming) "Naming conventions (programming)") for the guard [macro](https://en.wikipedia.org/wiki/Macro_(computer_science) "Macro (computer science)") may be used by different [programmers](https://en.wikipedia.org/wiki/Programmer "Programmer"). Other common forms of the above example include `GRANDPARENT_INCLUDED`, `CREATORSNAME_YYYYMMDD_HHMMSS` (with the appropriate time information substituted), and names generated from a [UUID](https://en.wikipedia.org/wiki/Universally_Unique_Identifier "Universally Unique Identifier"). (However, [names](https://en.wikipedia.org/wiki/Identifier_(computer_programming) "Identifier (computer programming)") starting with one underscore and a [capital letter](https://en.wikipedia.org/wiki/Capital_letter "Capital letter") or any name containing double underscore, such as `_GRANDPARENT__H` and `__GRANDPARENT_H`, are reserved to the language implementation and should not be used by the user.[[1]](https://en.wikipedia.org/wiki/Include_guard#cite_note-1)[[2]](https://en.wikipedia.org/wiki/Include_guard#cite_note-2))

Of course, it is important to avoid duplicating the same include-guard macro name in different header files, as including the 1st will prevent the 2nd from being included, leading to the loss of any declarations, inline definitions, or other #includes in the 2nd header.

## Difficulties

In order for #include guards to work properly, each guard must test and conditionally set a different preprocessor macro. Therefore, a project using #include guards must work out a coherent naming scheme for its include guards, and make sure its scheme doesn't conflict with that of any third-party headers it uses, or with the names of any globally visible macros.

For this reason, most C and C++ implementations provide a non-standard `[#pragma once](https://en.wikipedia.org/wiki/Pragma_once "Pragma once")` directive. This directive, inserted at the top of a header file, will ensure that the file is included only once. The [Objective-C](https://en.wikipedia.org/wiki/Objective-C "Objective-C") language (which is a superset of C) introduced an `#import` directive, which works exactly like `#include`, except that it includes each file only once, thus obviating the need for #include guards.[[3]](https://en.wikipedia.org/wiki/Include_guard#cite_note-3)

## Other languages

[PL/I](https://en.wikipedia.org/wiki/PL/I "PL/I") uses the `%INCLUDE` statement as the equivalent to C's `#include` directive. IBM Enterprise PL/I also supports the `%XINCLUDE` statement which will "incorporate external text into the source program if it has not previously been included." This differs from the C `#pragma once` in that the program including the external text is responsible for specifying that duplicate text should not be included, rather than the included text itself.

It also offers an `XPROCEDURE` statement, similar to a `PROCEDURE` statement, which will ignore the second and subsequent occurrences of an `XPROCEDURE` with the same name,[[4]](https://en.wikipedia.org/wiki/Include_guard#cite_note-4)

## See also

-   `[#pragma once](https://en.wikipedia.org/wiki/Pragma_once "Pragma once")`
-   [C preprocessor](https://en.wikipedia.org/wiki/C_preprocessor "C preprocessor")
-   [Circular dependency](https://en.wikipedia.org/wiki/Circular_dependency "Circular dependency")
-   [One Definition Rule](https://en.wikipedia.org/wiki/One_Definition_Rule "One Definition Rule")
-   [PL/I preprocessor](https://en.wikipedia.org/wiki/PL/I_preprocessor "PL/I preprocessor")

## References

-   C++ standard (ISO/IEC 14882) section 17.4.3.1.2/1

-   C standard (ISO/IEC 9899) section 7.1.3/1.

-   ["Objective C: Defining Classes"](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/DefiningClasses/DefiningClasses.html#//apple_ref/doc/uid/TP40011210-CH3-SW1). _developer.apple.com_. 2014-09-17. Retrieved 2018-10-03.

1.  IBM Corporation (August 2017). [_Enterprise PL/I for z/OS PL/I for AIX Enterprise PL/I for z/OS Language Reference Version 5 Release 1_](https://www.ibm.com/docs/en/SSY2V3_5.1.0/com.ibm.ent.pl1.zos.doc/lrm.pdf) (PDF). p. 257. Retrieved Apr 7, 2022.

## External links

-   [Include guard optimisation](https://web.archive.org/web/20100819052043/http://www.bobarcher.org/software/include/index.html)
-   [Redundant Include Guards](http://c2.com/cgi/wiki?RedundantIncludeGuards)