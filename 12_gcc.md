# Like Onions, Compilers Have Layers
### 9/24
---

### Compiling and Linking
 * Compilers are more complex than straightforward source code --> executable code translators. There are many steps involved, we will begin to peel back the layers of gcc so that we can better understand how to make more complex C programs. To start, we'll look at three major pieces of gcc, the __preprocessor__ __compiler__ and the __linker__.
 * Preprocessor
   * The preprocessor is, at it's simplest interpretation, a text replacement system.
   * It will actually modify your source code file with text, as opposed to binary data.
   * All preprocessor commands start with `#`, you've already been using the preprocessor with `#include <stdio.h>`
   * Note that preprocessor directives do not end in `;`
   * A few basic preprocessor directives
     * `#include`
       * Adds the entire text of the included file. This will add all of the function headers of a .h file at the position of the `#include`, which is why we put them at the top of a .c file.
     * `#define`
       * Usage: `#define TEXT REPLACEMENT`
       * Straightforward find and replace. Will replace every instance of `TEXT` with the provided `REPLACEMENT`.
       * A few examples:
       * `#define PI 3.14159`
       * `#define MESSAGE "Hello!"`
       * Note that define does not use `=`, becuase this is not an assignment. If you made the definitions above and later on had `printf("%s, %f\n", MESSAGE, PI);` the preprocessor would turn it into `printf("%s, %f\n", "Hello!", 31.14159);`. This would all happen before any of the C code is interpreted.
       * You can also use `#define` to declare function-like macros, we won't be doing this much, but it's good to be aware of:
         * `#define MAX(a, b) a > b ? a : b` Creates a macro that will create code to find the larger of two values (this makes use of the [ternary operator](https://en.wikipedia.org/wiki/%3F:)).
     * `#ifndef IDENTIFIER ... #endif`
       * A conditional preprocessor statement. If `IDENTIFIER` is not defined (for the preprocessor), then include all the lines of code up to the `#endif`. If `IDENTIFIER` is defined, skip everything up to the `#endif`.
       * If you only wanted to define `PI` if it was not defined elsewhere youd could do:
         ```C
         #ifndef PI
         #define PI 3.14159
         #endif
         ```
   * There are other preprocessor directives that we will not go into here.
 * Compiler
   * Turns C source code into binary code.
   * The result is __not__ an executable program.
   * Only one C file is compiled at a time.
   * If multiple files or external libraries are involved, they are compiled _separately_.
   * The compiler checks called functions against their declared hearders, but if a function is defined in a separate file, its code is not added at this step. This is where `#include` comes in. Since the preprocessor runs before the compiler, all the functions headers have already been added to your code.
   * `$ gcc -c <FILE>` will run the preprocessor and compile stages only, creating a non executable binary object file. The resulting file will have an extension of __.o__.
   * Since an executable is _not_ created, you can successfully compile, via `$ gcc -c`, a C file that does not have a `main` function.
 * Linker
   * Combines compiled binary code from multiple files into a single executable program.
   * Will automatically look for standard library source code, or anything that can be included using `<>`. This is why you can sucessfully compile a program that uses `printf()` without including `stdio.h`. The compiler gives a warning, because it has no function header to check against, but the linker knows where to find `printf()`, so as long as you used it correctly, it will fully compile.
   * If multiple definitions for any identifier is found, the linker will fail.
   * Since the goal of the linker is to create an executable file, it must find __one__ definition for `main`.
   * If you provide gcc multiple c files, it will compile each one individual and then run the linker.
   * If you provide gcc any .o files, it will skip the compilation step for those files and then use them during linking.
   * You can mix and match .c and .o files for gcc, but it is not encouraged. If you have a program made from multiple files, then you should either provide all the .c files to gcc, or create .o files for each and then put those into gcc.
   * For example these would be good ways to compile a program, if you had files `foo.c goo.c boo.c`:
     * `$ gcc foo.c goo.c boo.c`
     ```
     $ gcc -c foo.c
     $ gcc -c goo.c
     $ gcc -c boo.c
     $ gcc -o program foo.o goo.o boo.o
     ```
     * The second version is preferred because compiling each file separately allows for eaiser program development. I'm also using
---

### Assignment
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
 * Tomorrow, we will modify this process, at which point I'll ask to collect your work.
