### Loading A Shared Library Using `dlopen()`

In order to open and load the shared library, one should use the `dlopen()` function. It is used this way:  

```

#include <dlfcn.h>      /* defines dlopen(), etc.       */
.
.
void* lib_handle;       /* handle of the opened library */

lib_handle = dlopen("/full/path/to/library", RTLD_LAZY);
if (!lib_handle) {
    fprintf(stderr, "Error during dlopen(): %s\n", dlerror());
    exit(1);
}
```

  
The `dlopen()` function gets two parameters. One is the full path to the shared library. The other is a flag defining whether all symbols refered to by the library need to be checked immediatly, or only when used. In our case, we may use the lazy approach (`RTLD_LAZY`) of checking only when used. The function returns a pointer to the loaded library, that may later be used to reference symbols in the library. It will return `NULL` in case an error occured. In that case, we may use the `dlerror()` function to print out a human-readable error message, as we did here.