# GDB (GNU Debugger)

**Documentation:** [GDB](https://www.sourceware.org/gdb/)

GDB is GNU's debugging tool. 

## Getting started

GDB is available on Kestrel and supports a number of languages, including C, C++, and Fortran. 

To use GDB, first load it into your environment:

`module load gdb`

Second, make sure the program you are attempting to debug has been compiled with the `-g` debug flag and with the `-O0` optimization flag to achieve the best results with gdb.

One particularly useful feature of GDB is that it can be used to quickly examine the contents of a core dump file. The syntax for this feature is `gdb executable_name core_file_name`

For links to in-depth tutorials and walkthroughs of GDB features, please see [Resources](#resources).

## Availability

| Kestrel | Swift | Vermillion |
|:-------:|:-----:|:-----------|
|         |       |            |

## Resources

Gentle introduction to GDB: [here](https://www.cs.umd.edu/~srhuang/teaching/cmsc212/gdb-tutorial-handout.pdf)

Sample GDB session: [here](https://sourceware.org/gdb/current/onlinedocs/gdb.html/Sample-Session.html#Sample-Session)

"Print statement"-style debugging with GDB: [here](https://developers.redhat.com/articles/2021/10/05/printf-style-debugging-using-gdb-part-1#)
