### Automatic Startup And Cleanup Functions

Finally, the dynamic loading library gives us the option of defining two special functions in each library, namely `_init` and `_fini`. The `_init` function, if found, is invoked automatically when the library is opened, and before `dlopen()` returns. It may be used to invoke some startup code needed to initialize data structures used by the library, read configuration files, and so on.

The `_fini` function is called when the library is closed using `dlclose()`. It may be used to make cleanup operations required by the library (freeing data structures, closing files, etc.).

For an example of a program that uses the 'dl' interface, try looking at our [dynamic-shared library example directory](https://docencia.ac.upc.edu/FIB/USO/Bibliografia/dynamic-shared).

---