# [Make it so](https://www.youtube.com/watch?v=FaLyasJPyUU)
### 9/25
---

### Writing Multi-File C Programs
 * It is very common for C programs to make use of multiple files.
 * Normally, if there are multiple functions that work together, or deal with similar structures, those functions are put in a single .c file, and you create a .h file with the function headers.
 * It is standard practice to have a single .c file that contains `main`, followed by as many .c/.h file pairs needed.
 * For example, in the computer graphics course, we build a graphics engine, this requires a lot of code, which is broken up like so:
   * `main.c`: `main`
   * `matrix.c/.h`: matrix math code
   * `draw.c/.h`: shape drawing routines
   * `gmath.c/.h`: graphics specific math functions
   * `display.c/.h`: image displaying/saving code
   * `parser.c/.h`: code to parse drawing language created for the class.
 * When building such programs, the best strategy is to compile every .c file separately into .o files, then combine all the .o files together into one executable. Here is the example of this from yesterday's notes:
     ```
     $ gcc -c foo.c
     $ gcc -c goo.c
     $ gcc -c boo.c
     $ gcc -o program foo.o goo.o boo.o
     ```
 * This can get annoying, it certainly isn't as easy as `$ javac *.java`. If only there was a way to _make_ this better ...
---

### Make
 * Make is a command line tool designed to help automate building programs with multiple files and dependencies.
  * Make is designed so that it only compiles files that have been modified, or that rely on modified files.
 * Compiling instructions and file dependencies are put into a _makefile_.
 * When you run `$ make`, make will look for a file called _makefile_, you can specify a different file with the `-f` flag.
 * The main parts of makesfiles are:
   * Targets: Things to make (usually executables or .o files)
   * Dependencies: Files or other targets needed to create a target.
   * Rules: How to create the target.
   * Makefiles are generally broken up by __targets__, with associated rules and dependencies.
 * Make will always run the first target.
 * Make recursively goes through dependencies.
 * Make will check the modification timestamps for __targets__ and __dependencies__ and will only run the __rules__ if the target is older than one or more of it's dependencies.
 * Makefile Syntax:
   ```
   target: dependency0 dependency1 dependency2 ...
   TABrule
   ```
   * There should be a newline between the dependency list and the rules, and the __tab__ is necessary, there should not be any space between it and the rule.
 * Example
   * Here is a makefile for a program made from three .c files, main.c, foo.c and goo.c.
     * main.c calls functions from foo.c
     * foo.c calls functions from goo.c
     ```Makefile
     all: main.o foo.o goo.o
         gcc -o program main.o foo.o goo.o

     main.o: main.c foo.h
         gcc -c main.c

     foo.o: foo.c foo.h goo.h
         gcc -c foo.c

     goo.o: goo.c goo.h
         gcc -c goo.c
     ```
   * This makefile creates the executable file __program__.
   * Since _all_ is not a file and it is the first target, it will always run.
     * If instead, the first target was called __program__, then make would check the modification timestamp of that file.
   * __main.o__ is the first dependency, so make will go to that target.
   * __main.o__ depends on main.c and foo.h
     * Important note: main.c calls functions defined in foo.c. A common misconception is to make foo.c the dependency instead of foo.h. Why is it foo.h? Remember that gcc compiles one file at a time, and when functions are defined in other files, it only checks the headers, therefore foo.h is the dependency here.
     * Another way to think about it, main.c doesn't care _how_ the functions in foo.c are written, it just needs to match arguments and return types. foo.c could be totally rewritten, but if the headers stay the same, then main.c would not need to be recompiled.
   * The rest of the dependencies will go through in a similar way. Running `$ make` the first time would do the following:
     ```
     gcc -c main.c
     gcc -c foo.c
     gcc -c goo.c
     gcc -o porgram main.o foo.o goo.o
     ```
   * Notice the order of compilation and trace it through the makefile.
   * If goo.h is modified, the following would happen:
     ```
     gcc -c foo.c
     gcc -c goo.c
     gcc -o porgram main.o foo.o goo.o
     ```
---

### Assignment
 * Create a makefile for the assignment from yesterday. Here it is again:
 * Yesterday I asked you to write 3 functions. Today I would like you to create a multiple file c program based on those functions. Your program should consist of:
   1. A .c file containing your `main` function that tests your code.
   2. A .c file containing your defined functions from yesterday.
   3. A .h file containing the headers for your functions.
      * An example header file:
      ```C
      double average(int *arr, int size);
      void arr_copy(int *a0, int *a1, int size);
      int mystrlen(char *s);
      ```
      * Your function names and arguments may differ, but your .h should look like this.
 * After you've broke up your code into these three files, create an executable by compiling your two .c files separately and then combinging the resulting .o files.
