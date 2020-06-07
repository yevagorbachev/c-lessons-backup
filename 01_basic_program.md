# Compiling your C Knowledge

### Administrative Stuff
 * A big thank you to Mr. Holmes for stepping in yesterday for all my classes!
 * Thank you to everyone that has filled out the information survey. As of this writting, I have ~~79~~ 91 responses!
 * I will be getting the google group QAF up and running sometime today. Be on the lookout for an invitation to the group via your stuy.edu email. The QAF will probably be quite helpful over the weeeked as you get started working in C.
---

### Ye Olde "Hello World"

```C
int main() {
  printf("Good News Everyone!\n");
  return 0;
}
```

* This is a simple C program, that will compile and run.
* Think about the most basic of Java programs, compare that to this. What things are similar? What are some differences?
---

### C Quickstart
* C program files are _mostly_ a series of function definitions. As C is not an OOP language, there is no class-like structural overhead.
* Like in Java, `main` is a special function, it is the only function that runs at program execution. Of course, any functions called from within `main` will also be run.
* C is a statically typed langauge, meaning identifiers (variables and functions) must be given a type when they are declared. 
    * You'll notice that in the above example, `main` has an `int` return type. This is the standard for C (as opposed to Java's `void`), though if you use another type the program will compile (more on that later).
    * The types are similar to those in Java, with a few notable exceptions. For the moment, use `int` for integers and `double` for floating point values. Don't even think about dealing with string yet (remember, no objects...).
* `main` should have a return type of `int`. This can be used later on to check if a program executed successfully. By convention, a return value of 0 means everything went as planned.

### Wirting, compiling, and running
 * By convention, C source files should have a `.c` file extension (i.e. `dylan.c`).
 * The C compiler we will be using is __gcc__ (the Gnu C Compiler)
   * usage: `$ gcc dylan.c`
     * This will create a standalone executable file.
     * The default name for the output file is `a.out`
     * There is no preferred extension for c executable files (think about programs like `ls`, `ssh`, `chmod`, these are all C programs, notice the lack of file extension).
     * You can provide your own output file name with the `-o` flag.
       * usage: `$ gcc -o dj dylan.c`
 * Compiled C programs are natively executable, to run them just type `./program` (i.e. `$ ./a.out` or `$ ./dj`
   * The `./` is only needed because you probably compiled the file in a folder outside your PATH environment variable (if that is unclear, you can forget the previous sentence entirely for now).
 * Before moving on, you should write, compile and run the example program provided above. I promise it is 100% sytactically correct. (Yes, you may get a compiler warning message, this is the only time you're allowed to ignore it.
 
### `printf`: The thinking person's `System.out.println`
  * `printf` is the function normally used in C to print to standard out.
  * usage: `printf( string, arg0, arg1, ...)`
     * Sends `string` to standard out. 
     * The first argument must be a literal string enclosed by `"`, as in the example program above.
     * `string` can contain special placeholder charaters that are used to insert other values into the output.
     * `%d` is the placeholder to display a value as an `int`.
     * `%lf` is the placeholder to display a value as a `double`.
     * There are other placeholder characters that we will see later on.
     * If placeholder characters are used, then they will be replaced by the arguemnts following the string when `printf` is executed.
     * The value arguemnts can be either variables or literal values.
     * example: `printf(“these are numbers: %d %lf\n”, 3, 845.273);` would display: `these are numbers: 3 845.273`
   * Once you get used to it, most people prefer `printf`'s value replacement system to Java's string concatenation (+) inside `System.out.println`. In fact, Java does have a `System.out.printf` because of it.
   * There is one difference between `System.out.println` and `printf` that you will find annoying. I leave it for you to discover...
   * As an exercise, add some `printf` statements to your existing example program. Try declaring variables and printing their values. Once you get the hang of it, try using the wrong formatting characters, see what happens...
   * | Type | Placeholder |
     |------|-------------|
     |`int` | `%d`        |
     |`long`| `%ld`       |
     |`float`| `%f`*       |
     |`double`| `%lf`*     |
     |`char`| `%c`         |
     |string| `%s` |
     |pointer| `%p`|
   * \* `%0.xf` or `%0.xlf` will print `x` significant digits after the floating point 
---
### Assignment
Get your home computer setup to compile and run C programs. If you need help check out the [Class Resources page](http://www.stuycs.org/courses/mks65/resources). It also is a great time to get started using the __QAF__
