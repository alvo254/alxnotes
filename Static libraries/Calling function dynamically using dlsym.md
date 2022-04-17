### Calling Functions Dynamically Using `dlsym()`

After we have a handle to a loaded shared library, we can find symbols in it, of both functions and variables. We need to define their types properly, and we need to make sure we made no mistakes. The compiler won't be able to check those declarations, so we should be extra carefull when typing them. Here is how to find the address of a function named 'readfile' that gets one string parameter, and returns a pointer to a `'struct local_file'` structure:

---

```

/* first define a function pointer variable to hold the function's address */
struct local_file* (*readfile)(const char* file_path);
/* then define a pointer to a possible error string */
const char* error_msg;
/* finally, define a pointer to the returned file */
struct local_file* a_file;

/* now locate the 'readfile' function in the library */
readfile = dlsym(lib_handle, "readfile");

/* check that no error occured */
error_msg = dlerror();
if (error_msg) {
    fprintf(stderr, "Error locating 'readfile' - %s\n", error_msg);
    exit(1);
}

/* finally, call the function, with a given file path */
a_file = (*readfile)("hello.txt");
```

---

As you can see, errors might occur anywhere along the code, so we should be carefull to make extensive error checking. Surely, you'll also check that 'a_file' is not `NULL`, after you call your function.