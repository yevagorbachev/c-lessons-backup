# Writing Functioning Code
## 9/13

### Administrative Stuff
 * I may have spoekn too soon with respect to github classroom. It's made my github organization very cluttered. Will evaluate over the weekend.
---

### Declaring & Defining Functions
 * Function and variable names are both examples or _identifiers_.
 * All identifiers must be declared before they can be used.
   * For vairables, this means providing the name and type before using a variable in an expression. (i.e. `char c;`)
   * Of course with vairables, we have the option of declaring and _initializing_ on the same line. (i.e. `char c = 'x'`)
 * A function declaration provides its return type, name and parameters. This is also known as a function _header_.
   * `double dylan(int jack);`
   * Function declrations on their own do not have a body. Note the `;` at the end of the example above.
 * Function definitions are the bodies of functions.
   * Similar to vairables functions can be declared and defined at the same time.
   * In fact, you cannot provide a function definition without the header.
 * Functions must be declared before being used.
   * In an early stage of compilation, gcc looks up any function that is used and compares that usage to the function declaration. This checks that you are providing the correct parameters and using the return value appropriately.
   * Remember the warning you got about using `printf` before you knew about `#include`?. That was becuase you used a function but without the function declaration, gcc was unable to check that you used it correclty.
 * There are three ways to handle function declarations.
   1. Always declare and define functions at the same time.
      * This is the simplest solution. It is good when you don't have many functions to work with and if you don't forsee using those functions in other programs.
      ```C
      char funky(int x) {
          return x % 256;
      }
      void town(int i) {
          for (; i; i--)
            printf("%c\n", funky(i));
      }
      ```
      * One of the biggest problems with this method is that you have to keep track of the order you write your functions in if they call each other. This can get logistically difficult.
   2. Write the function declarations at the top of your code (after any `#include` statemants), then define the functions later.
     * When providing the definitions, you will still need to repeat the header.
     * Major benefit to this method is that you do not need to worry about the order for defining the functions. Since you've declared them all ahead of time, you're in the clear.
     ```C
     char funky(int x);
     void town(int i);

     <function definitions later>
     ```
     * This method works very well, and is reccomended if you are writing numerous functions.
     * This method is not ideal if you want to write a library of functions that can be used in multiple programs.
   3. Put all the functions headers in a separate file, then provide the definitions in another file. You can use these headers via the `include` statement.
     * This is what you're doing with `#include <stdio.h>` and similar statements.
     * System header files use `<>`, custom header files use `""`.
     * We'll go over this method in more detail later.
---

### Assignment
 * If you followed along with yesterday's lesson, then you should have a single C file that contains separate functions to solve a few project euler problems.
 * Modify that file so that you declare all your functions using headers before providing the definitions later (method 2 from above).
 * Your program should compile and run, providing the answers to the project euler problems.
 * I will want to collect this, but will hold off until I look into classroom more.
