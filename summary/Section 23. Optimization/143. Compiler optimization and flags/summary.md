# Program optimization
Optimization is a series of actions taken by the compiler on your program's code generation process to reduce
- Number of instructions (code space optimization)
- Memory access time (time space optimization)
- Power consumption
  
By default, the compiler doesn't invoke any optimization on your program

You can enable the optimization using compiler flags.

# GCC compiler flags to enable optimization
- **-O0**: No optimization
  - Not recommended for productions if you have limited code and ram space
  - Has fastest compilation time
  - This is debugging friendly and used during development
  - A code which works with -O0 optimization may not work with -O0+ optimization levels. Code needs to be verified again.
- **-O1**: Optimize for code size and execution time
  - This is the default optimization level
  - This is the best optimization level for most of the applications
  - This optimization level is recommended for production code
- **-O2**: Full optimization
  - Slow compilation time
  - Not debugging friendly
- **-O3**: full optimization of -O2 + some more aggressive optimization steps will be taken by the compiler
  - Slowest compilation time
  - May cause bugs in the program
  - Not debugging friendly