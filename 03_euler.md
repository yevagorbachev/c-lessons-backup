# Time to do some work!
## 9/11

### Administrative Stuff
 * I know the computers were down on Monday, so I did not provide a new lesson for Tuesday. I've been informed things are back up and running.
 * Today will be your first programming assignment that I will collect. I'm going to try github classroom, more on that below.
 * I will also start dating these lessons, as you can see above.
 * As of this writting, there are ~27~ 6 pending invitations to the QAF, not bad, but I hope that number goes down to 0 by tomorrow!
 * There is currently no traffic on the QAF yet, so I will assume you all were able to successfully write, compile, and run a C program on your computers. (This would be a first)
---

### include
 * In the example program from lesson 01, you shoudl have notice a warning from gcc about `printf`.
 * The warning (not error, which is why it still compiles), is because you are using a function, `printf`, that you have neither declared nor defined.
 * The program compiles because `printf` is part of the standard c library, and gcc is smart enough to look in the standard c library when compiling.
 * We will go into more detail on what happens at compilation later, for now, I don't want you to get used to warnings and letting them pass, so let's fix this one.
 * `include` is a keyword (technically a c pre-processor instruction), that allows you to access function and variable declarations from other files. 
 * `include` statments should always go at the top of your program, with 1 file per line.
 * Use `<>` to include files in standard libraries.
 * Use `""` to include other files (such as files you've written).
 * Example: `#include <stdio.h>`
   * This will include the function declarations in the stdio (standard input/output) library. `printf` lives here.
   * The `#` is necessary before anything else.
 * Most c programs will start off with:
   ```C
   #include <stdio.h>
   #include <stdlib.h>
   ```
---

### Control Structures
 * C has the same basic control structures as java: `if, else if, else, while, for, do ... while`
   * Quick note on `for`: Do not declare your counter variable in the loop.
     * `for( x=0; x < 10; x++)` Totally cool.
     * `for( int x=0; x < 10; x++)` no bueno.
 * Remember that in C, __all numbers are boolean values__, 0 is false, everything else is true.
 * How important is this? Well look at the following statement:
   * `if ( x = 0 )`
   * Upon first glance, maybe it seems fine, maybe you notice the incredibly common programming typo.
   * javac would never let this fly. Then again, javac assumes you are an idiot and that you have no idea how to program.
   * gcc thinks this is totally cool. gcc thinks you are a master programmer (perhaps even a 1337 hax0r), and you meant to do this.
   * C interprets this statement as follows:
     1. Assign variable x the value 0.
     2. The assignment operator returns the value assigned, so the statement will return 0.
     3. 0 is false, so the if statement will fail.
---

### Functions
 * Function headers in C have the following format:
   * return_type name( parameters )
 * Similar to java, without all that object oriented junk.
 * The rule is you must declare functions before using them. We'll go into more detail on this later.
 * For now, if you want to write functions to use in `main`, write the function above the declaration of `main`.
---

### Assignment
 * Look at the problems here: http://projecteuler.net/index.php?section=problems
 * They are all math problems of some sort, pick two and write a c program to solve them
   * Some good starters are problems 1, 5 and 6
   * Finished early? pick a third, a fourth, a fifth...
 * We're going to try github classroom, I believe I have set up the assignment successfully.
 * To start, follow this link: https://classroom.github.com/a/DDj-1Y92
