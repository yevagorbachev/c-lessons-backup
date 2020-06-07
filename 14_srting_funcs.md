# How Funky Are Your Strings?
### 9/26
---

### ADministrative Stuff
 * This time next week, I'll be back. We will definitely spend some class time going over things and hopefully clarifying any questions you have about the material covered up until then.
 * I said I was going to collect the makfile version of the function assignment, then forgot to set that up. Please submit that assignment here: https://classroom.github.com/a/Sm2_ZfAH
---

### String Library Functons
 * A few days agao I asked you to look up some of the functions in `string.h`. We will go over these today, so that everyone is clear on how they work.
 * Some general notes on these functions:
   * Generally, they __assume__ you are using `NULL` terminated strings when providing arguments. If you do not, then all bets are off. When building your own strings, make sure they are always `NULL` terminated.
   * In functions that copy or concatenate strings, it is up to you to make sure there is enough room is the destination `char` array for the new data. How important is it? Heed this warning from the man page for `strcpy` (emphasis added):

      > If the destination string of a strcpy() is not large enough, then anything might happen. Overflowing fixed-length string buffers is a favorite cracker technique for taking complete control of the machine.  Any time a program reads or copies data into a buffer, the program first needs to check that there's enough space. This  may be unnecessary if you can show that overflow is impossible, but be careful: programs can get changed over time, __in ways that may make the impossible possible__.

   * To help deal with this potentially specatcular program flaw, the standard string functions often have an `n` variant (i.e. `strcpy` and `strncpy`). The purpose of the `n` variant is to provide an extra numeric argument representing the fartherst you want to go. If used correctly, this will prevent string buffer overflows.
 * `strlen(char *s)`
   * Returns the length of the string `s`, up to, but _not including_, the terminating `NULL`.
   * Note that this is just the number of `chars` in `s` before `NULL`, it does not provide the overall size of the actual array.
 * `strcpy(char *dest, char *src)` | `strncpy(char *dest, char *src, size_t n)`
   * Copies the string `src` into the `char` array `dest`, including the terminating `NULL`.
   * Returns a pointer to `dest`.
   * In `strncpy`, at most, `n` `chars` are copied. If there is no terminating `NULL` by the `n`th byte, then `dest` will not be `NULL` terminated. If `n` is longer than `src` (meaning that the terminating `NULL` of `src` shows up before `n` total characters), then `strncpy` will fill in `NULL` characters until `n` total characters have been copied.
   * `size_t` is not a real data type, it is really an `unsigned long`.
 * `strcat(char *dest, char *src)` | `strncat(char *dest, char *src, size_t n)`
   * Appends a copy of the string `src` to the end of `dest`, starting by overwritting the terminating `NULL` of `dest` with the first character of `src`.
   * Will add a terminating `NULL` if one appears in `src`.
   * `strncat` will append at most `n` characters, and will always add a terminating `NULL` after the `n`th character.
   * If you are using `strncat`, keep in mind that `n` is the number of characters to copy over, not the total size of the concatenated string. Therefore `dest` must be large enough to hold `strlen(dest) + n + 1` characters (the 1 standing for the always included `NULL`).
 * `strcmp(char *s1, char *s2)`
   * Compares `s1` to `s2`, returning:
     * `0` if `s1` and `s2` are the same (up to the terminating `NULL`).
     * A negative integer if `s1` is less than `s2`
     * A positive integer is `s1` is greater than `s2`
   * `strcmp` is only concerned with the characters up to `NULL`, it is possible that the underlying arrays for `s1` and `s2` have differences after that point, but if they are strings, we generally don't care about that data anyway.
   * "less than" and "greater than" are measured by numeric `char` values (remember that `char` is an integer data type), comparing each `char` consecutively until they do not match or `NULL` is found. Some examples:
     * `"bat"` is greater than `"Bat"`.
     * `"it"` is less than `"item"`
 * `strchr(char *s, char c)`
   * Returns a __pointer__ to the first time `c` appears in `s`, or `NULL` (`0`) if `c` is not found in `s`.
   * A common misconception is that this returns the index of `c`, once again, it returns a pointer to where `c` is found in `s`. (the index could be calculated by subtrating `s` from the return value though).
 * `strstr(char *haystack, char *needle)`
   * Returns a __pointer__ to the first time the string `needle` appears in `haystack`, or `NULL`, if it is not found.

---

### Assignment
 * This is your first larger assignment.
 * This will be due next week, probably Thursday morning considering the holidays on Monday and Tuesday.
 * Were I in class, I would stricktly enforce this as a pair assignment. I still consider this a pair assignment, so you should work with one other person.
 * First, acquaint yourself with the basic string functions: strlen, strcpy, strcat, strncat and strncpy. You can look at the man pages for each if you are unclear as to their uses. I encourage you to play around with each so you are comfortable with how to use them.
 * Then write your own versions of the following:
 * Required (use the function headers I provide, they may differ from the standard headers).
   * strlen [ `int strlen( char *s )` ]
   * strcpy/strncpy (choose one)  [ `char * strcpy( char *dest, char *source )`  `char * strncpy( char *dest, char *source, int n)`  ]
   * strcat/strncat (choose one)  [ `char * strcat( char *dest, char *source )`  `char * strncat( char *dest, char *source, int n)`  ]
   * strcmp  [ `int strcmp( char *s1, char *s2 )` ]
     * Your version does not need to return the same exact value as the system version, as long as it returns -, + or 0 when it should.
   * strchr  [ `char * strchr( char *s, char c )` ]
 * You must test every function you write, you will not get full credit for an untested functions.
 * You do not need to write 7 functions, only 5, but you need to write 1 of the "n" versions. (So if you do strcpy then you have to do strncat)
 * Your program should consist of a .c file containing `main` with all your tests, along with a .c/.h pair of files for your string functions.
 * Extra functions:
   * The other strn/str version of the functions you wrote above
   * strstr [ `char * strstr( char *s1, char * s2 )` ]
 * When you test your functions,  run them alongside the regular ones so you can see if they behave the same way or not. Remember you should call them something other than the regular names.

 * Here's an example of what your code might look like when run:
  ```
  s1: [?
  ?W?]
  s2: [hello]
  s3: [goodbye]

  Testing strlen(s2):
  [standard]: 5
  [mine]: 5

  Testing strcpy(s1, s2):
  [standard]: [hello]
  [mine]: [hello]

  Testing strncpy(s1, s3, 3):
  [standard]: [goolo]
  [mine]: [goolo]

  Testing strcat(s1, s3):
  [standard]: [goologoodbye]
  [mine]: [goologoodbye]

  Testing strncat(s1, s2, 3):
  [standard]: [goologoodbyehel]
  [mine]: [goologoodbyehel]

  Testing strchr(s1, 'l'):
  [standard]: [0x7fff57d70a13]
  [mine]: [0x7fff57d70a13]

  Testing strchr(s1, 0):
  [standard]: [0x7fff57d70a1f]
  [mine]: [0x7fff57d70a1f]

  Testing strchr(s1, 'z'):
  [standard]: [0x0]
  [mine]: [0x0]

  Testing strcmp
  Comparting ab to abc:
  [standard]: [-99]
  [mine]: [-99]
  Comparting abc to ab:
  [standard]: [99]
  [mine]: [99]
  Comparting abc to abc:
  [standard]: [0]
  [mine]: [0]
  ```
