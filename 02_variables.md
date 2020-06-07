# Variables are the spice of life.

### Administrative Stuff
 * As of this writting, there are 27 pending invitations to the QAF, not bad, but I hope that number goes down to 0 by tomorrow!
 * There is currently no traffic on the QAF yet, so I will assume you all were able to successfully write, compile, and run a C program on your computers. (This would be a first)
---

### Primative Data Types
 * All C primatives are _numeric_ types, __ALL__.
 * The only difference is the size of the variable and whether it is an integer or floating point.
 * Size _can_ be platform dependant, but there are gneral standards.
   * `sizeof( type )` will return the size of a data type _or_ variable.
 * | Type   | Size (Bytes)   | Range (all boundries are inclusive)  |
   | ---    | ---            | ---     |
   | `char` | 1              | [-128, 127] |
   | `short`| 2              | [-32,768, 32,767] |
   | `int`  | 4              | [-2^31, 2^31 - 1] |
   | `long` | 8              | [-2^63, 2^63 - 1] |
   | `float`| 4              | 7 digits of precision |
   | `double`| 8             | 14 digits of precision |
 * `char` is an integer type, but can be used to refer to character literals as well.
   * `char c = 97;` and `char c = 'a';` are both equally valid statements.
   * This also means you can perform arithmetic operations on chars natively.
 * Note there is no boolean type. In c, any number is a boolean value:
   * __0 is false__
   * __All other numeric values are true__
---

### Variables in C
 * C is staticallly typed, meaning every variable must be given a type.
 * Variables must be declared before they are used.
   * You can assign a variable a value at declaration (i.e. `int x = 10;`)
 * _THERE IS NO DEFAULT VALUE FOR VARIABLES_
   * In Java, everything got initialized to 0, that's a thing of the past.
   * Remember that declaring a vairable means requesting a piece of memory to be used by your program of the corresponding vairable size. (`int` means you are asking for 4 bytes of memory.)
   * If you do not initialize (provide a value for) a variable, it's initial value will be wahtever happens to be in the piece of memory that was assigned to your variable. Sometimes, that's 0, sometimes it's 2167354. Who knows?
   * This is cause for one of the most frustrating kind of programming errors in C. Normally, if you run the same program twice, you will get the saem result. If you don't initialize a variable, you could run the same program twice and get two different results, because you're not guranteed that variable will have had the same value twice (common occurance: you run your program and get lucky, a variable is initialized to 0. Then I run your work and the program crashes or does not give the required result because the variable is initialized to some junk value).
 * Variables can be declared as `unsigned` (i.e. `unsigned int u;`).
   * `unsigned` variables have a lower bound of 0 and a higher upper bound than their signed counterparts.
   * `unsigned char uc;` declares a 1 byte integer type that can hold any number in the range [0, 255] otherwise known as [0, 2^8 - 1], as in there are 8 bits used for the number.
   * `unsigned` variables don't need to set aside a bit for the sign of the value, hence the larger upper bound.
___

### Assignment
 * Play around with vairables, types and printf.
   * Use a few different types.
   * Try out some `unsigned` integer types.
   * Try going out of bounds on either end. This is easiest to work with using `char` or `short`.
   * gcc is will let you do things that javac would never condone. You can start to get the feel for that here.
 * Get your home computer setup to compile and run C programs. If you need help check out the [Class Resources page](http://www.stuycs.org/courses/mks65/resources). It also is a great time to get started using the __QAF__
