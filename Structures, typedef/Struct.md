# struct (C programming language)

From Wikipedia, the free encyclopedia

[Jump to navigation](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#mw-head) [Jump to search](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#searchInput)

A **struct** in the [C programming language](https://en.wikipedia.org/wiki/C_programming_language "C programming language") (and many derivatives) is a [composite data type](https://en.wikipedia.org/wiki/Composite_data_type "Composite data type") (or [record](https://en.wikipedia.org/wiki/Record_(computer_science) "Record (computer science)")) declaration that defines a physically grouped list of variables under one name in a block of memory, allowing the different variables to be accessed via a single [pointer](https://en.wikipedia.org/wiki/Pointer_(computer_programming) "Pointer (computer programming)") or by the struct declared name which returns the same address. The struct data type can contain other data types so is used for mixed-data-type records such as a hard-drive directory entry (file length, name, extension, physical address, etc.), or other mixed-type records (name, address, telephone, balance, etc.).

The C struct directly references a _contiguous block_ of physical memory, usually delimited (sized) by word-length boundaries. It corresponds to the similarly named feature available in some [assemblers](https://en.wikipedia.org/wiki/Assembly_language "Assembly language") for Intel processors. Being a block of contiguous memory, each field within a struct is located at a certain fixed offset from the start.

Because the contents of a struct are stored in contiguous memory, the [sizeof](https://en.wikipedia.org/wiki/Sizeof "Sizeof") operator must be used to get the number of bytes needed to store a particular type of struct, just as it can be used for [primitives](https://en.wikipedia.org/wiki/Primitive_data_type "Primitive data type"). The alignment of particular fields in the struct (with respect to [word](https://en.wikipedia.org/wiki/Word_(computer_architecture) "Word (computer architecture)") boundaries) is implementation-specific and may include padding, although modern compilers typically support the `#pragma pack` directive, which changes the size in bytes used for alignment.[[1]](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#cite_note-1)

In the [C++](https://en.wikipedia.org/wiki/C%2B%2B "C++") language, a struct is identical to a [C++ class](https://en.wikipedia.org/wiki/C%2B%2B_classes "C++ classes") but has a different default visibility: class members are private by default, whereas struct members are public by default.

## Contents

-   [1 In other languages](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#In_other_languages)
-   [2 Declaration](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#Declaration)
-   [3 Initialization](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#Initialization)
-   [4 Assignment](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#Assignment)
-   [5 Pointers to struct](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#Pointers_to_struct)
-   [6 See also](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#See_also)
-   [7 References](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#References)

## In other languages

The struct data type in C was derived from the [ALGOL 68](https://en.wikipedia.org/wiki/ALGOL_68 "ALGOL 68") struct data type.[[2]](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#cite_note-sigplan-2)

Like its C counterpart, the struct data type in [C#](https://en.wikipedia.org/wiki/C_Sharp_(programming_language) "C Sharp (programming language)") (_Structure_ in [Visual Basic .NET](https://en.wikipedia.org/wiki/Visual_Basic_.NET "Visual Basic .NET")) is similar to a [class](https://en.wikipedia.org/wiki/Class_(computer_programming) "Class (computer programming)"). The biggest difference between a struct and a class in these languages is that when a struct is passed as an argument to a function, any modifications to the struct in that function will not be reflected in the original variable (unless pass-by-reference is used).[[3]](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#cite_note-3)

This differs from C++, where classes or structs can be statically allocated or dynamically allocated either on the stack (similar to C#) or on the heap, with an explicit pointer. In [C++](https://en.wikipedia.org/wiki/C%2B%2B "C++"), the only difference between a struct and a [class](https://en.wikipedia.org/wiki/C%2B%2B_classes "C++ classes") is that the members and base classes of a struct are [public](https://en.wikipedia.org/wiki/Access_modifiers "Access modifiers") by default. (A class defined with the `class` keyword has [private](https://en.wikipedia.org/wiki/Access_modifiers "Access modifiers") members and base classes by default.)

## Declaration

The general syntax for a struct declaration in C is:

struct tag_name {
 type member1;
 type member2;
 /* declare as many members as desired, but the entire structure size must be known to the compiler. */
};

Here `tag_name` is optional in some contexts.

Such a `struct` declaration may also appear in the context of a [typedef](https://en.wikipedia.org/wiki/Typedef "Typedef") declaration of a type alias or the declaration or definition of a variable:

typedef struct tag_name {
 type member1;
 type member2;
} struct_alias;

## Initialization

There are three ways to initialize a structure. For the `struct` type

/* Declare the struct with integer members x, y */
struct point {
 int x;
 int y;
};

_C89-style initializers_ are used when contiguous members may be given.[[4]](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#cite_note-4)

/* Define a variable p of type point, and initialize its first two members in place */
struct point p = { 1, 2 };

For non contiguous or out of order members list, _designated initializer_ style[[5]](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#cite_note-5) may be used

/* Define a variable p of type point, and set members using designated initializers */
struct point p = { .y = 2, .x = 1 };

If an initializer is given or if the object is [statically allocated](https://en.wikipedia.org/wiki/Static_memory_allocation "Static memory allocation"), omitted elements are initialized to 0.[[6]](https://en.wikipedia.org/wiki/Struct_(C_programming_language)#cite_note-6)

A third way of initializing a structure is to copy the value of an existing object of the same type

/* Define a variable q of type point, and set members to the same values as those of p */
struct point q = p;

## Assignment

A struct may be assigned to another struct. A compiler might use `memcpy()` to perform such an assignment.

struct point {
 int x;
 int y;
};

int main(void)
{
 struct point p = { 1, 3 }; /* initialized variable */
 struct point q; /* uninitialized */
 q = p; /* copy member values from p into q */
 return 0;
}

## Pointers to struct

Pointers can be used to refer to a `struct` by its address. This is useful for passing structs to a function. The pointer can be [dereferenced](https://en.wikipedia.org/wiki/Dereference_operator "Dereference operator") using the `*` operator. The `->` operator dereferences the pointer to struct (left operand) and then accesses the value of a member of the struct (right operand).

struct point {
 int x;
 int y;
};
struct point my_point = { 3, 7 };
struct point *p = &my_point; /* p is a pointer to my_point */
(*p).x = 8; /* set the first member of the struct */
p->x = 8; /* equivalent method to set the first member of the struct */

## See also

-   [Bit field](https://en.wikipedia.org/wiki/Bit_field "Bit field")
-   [Flexible array member](https://en.wikipedia.org/wiki/Flexible_array_member "Flexible array member")
-   [Passive data structure](https://en.wikipedia.org/wiki/Passive_data_structure "Passive data structure")
-   [Union type](https://en.wikipedia.org/wiki/Union_type "Union type")

## References

-   ["Struct memory layout in C"](https://stackoverflow.com/questions/2748995/struct-memory-layout-in-c). _Stack Overflow_.

-   [Ritchie, Dennis M.](https://en.wikipedia.org/wiki/Dennis_Ritchie "Dennis Ritchie") (March 1993). ["The Development of the C Language"](http://www.bell-labs.com/usr/dmr/www/chist.html). _ACM SIGPLAN Notices_. **28** (3): 201–208. [doi](https://en.wikipedia.org/wiki/Doi_(identifier) "Doi (identifier)"):[10.1145/155360.155580](https://doi.org/10.1145%2F155360.155580). The scheme of type composition adopted by C owes considerable debt to Algol 68, although it did not, perhaps, emerge in a form that Algol's adherents would approve of. The central notion I captured from Algol was a type structure based on atomic types (including structures), composed into arrays, pointers (references), and functions (procedures). Algol 68's concept of unions and casts also had an influence that appeared later.

-   ["Parameter passing in C#"](http://yoda.arachsys.com/csharp/parameters.html).

-   Kelley, Al; Pohl, Ira (2004). [_A Book On C: Programming in C_](https://archive.org/details/bookoncprogrammi00kell/page/418) (Fourth ed.). pp. [418](https://archive.org/details/bookoncprogrammi00kell/page/418). [ISBN](https://en.wikipedia.org/wiki/ISBN_(identifier) "ISBN (identifier)") [0-201-18399-4](https://en.wikipedia.org/wiki/Special:BookSources/0-201-18399-4 "Special:BookSources/0-201-18399-4").

-   ["IBM Linux compilers. Initialization of structures and unions"](https://www.ibm.com/support/knowledgecenter/en/SSLTBW_2.3.0/com.ibm.zos.v2r3.cbclx01/strin.htm).

1.  ["The New C Standard, §6.7.8 Initialization"](http://c0x.coding-guidelines.com/6.7.8.html#1695).

[Categories](https://en.wikipedia.org/wiki/Help:Category "Help:Category"):

-   [C (programming language)](https://en.wikipedia.org/wiki/Category:C_(programming_language) "Category:C (programming language)")