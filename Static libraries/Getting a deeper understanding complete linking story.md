### The Importance Of Linking Order

In order to fully understand the way linking is done, and be able to overcome linking problems, we should bare in mind that the order in which we present the object files and the libraries to the linker, is the order in which the linker links them into the resulting binary file.

The linker checks each file in turn. If it is an object file, it is being placed fully into the executable file. If it is a library, the linker checks to see if any symbols referenced (i.e. used) in the previous object files but not defined (i.e. contained) in them, are in the library. If such a symbol is found, the whole object file from the library that contains the symbol - is being added to the executable file. This process continues until all object files and libraries on the command line were processed.

This process means that if library 'A' uses symbols in library 'B', then library 'A' has to appear on the link command before library 'B'. Otherwise, symbols might be missing - the linker never turns back to libraries it has already processed. If library 'B' also uses symbols found in library 'A' - then the only way to assure successful linking is to mention library 'A' on the link command again after library 'B', like this:  
  
`$(LD) ....... -lA -lB -lA`  
  
This means that linking will be slower (library 'A' will be processed twice). This also hints that one should try not to have such mutual dependencies between two libraries. If you have such dependencies - then either re-design your libraries' contents, or combine the two libraries into one larger library.

Note that object files found on the command line are always fully included in the executable file, so the order of mentioning them does not really matter. Thus, a good rule is to always mention the libraries after all object files.

---

### Static Linking Vs. Dynamic Linking

When we discussed static libraries we said that the linker will try to look for a file named 'libutil.a'. We lied. Before looking for such a file, it will look for a file named 'libutil.so' - as a shared library. Only if it cannot find a shared library, will it look for 'libutil.a' as a static library. Thus, if we have created two copies of the library, one static and one shared, the shared will be preferred. This can be overridden using some linker flags (`'-Wl,static'` with some linkers, `'-Bstatic'` with other types of linkers. refer to the compiler's or the linker's manual for info about these flags).