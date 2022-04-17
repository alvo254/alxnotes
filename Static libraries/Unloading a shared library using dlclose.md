### Unloading A Shared Library Using `dlclose()`

The final step is to close down the library, to free the memory it occupies. This should only be done if we are not intending to use it soon. If we do - it is better to leave it open, since library loading takes time. To close down the library, we use something like this:  
  
`dlclose(lib_handle);`  
  
This will free down all resources taken by the library (in particular, the memory its executable code takes up).