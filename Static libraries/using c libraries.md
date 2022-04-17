---

## Using A "C" Library In A Program
After we created our archive, we want to use it in a program. This is done by adding the library's name to the list of object file names given to the linker, using a special flag, normally `'-l'`. Here is an example:  
  
`cc main.o -L. -lutil -o prog`  
  
This will create a program using object file "main.o", and any symbols it requires from the "util" static library. Note that we omitted the "lib" prefix and the ".a" suffix when mentioning the library on the link command. The linker attaches these parts back to the name of the library to create a name of a file to look for. Note also the usage of the `'-L'` flag - this flag tells the linker that libraries might be found in the given directory ('.', refering to the current directory), in addition to the standard locations where the compiler looks for system libraries.

For an example of program that uses a static library, try looking at our [static library example directory](https://docencia.ac.upc.edu/FIB/USO/Bibliografia/static-lib).