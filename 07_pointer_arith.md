# Pointed Debate.
## 9/17

### Administrative Stuff
---

### Pointer Arithmetic
 * Non-pointer variables have different types in order to differentiate integer/floating point and memory size.
 * Pointer variables are always unsigned integer types and are all the same size.
 * So why do we declare pointers of different types (`char *`, `int *`, `double *` ...)?
 * The answer is __pointer arithmetic__.
 * You can perform the following arithmetic operations on pointers.
   * `+ - ++ --`
   * Other arithmetic operators will not work.
 * When you perform arithmetic on pointers, the operations are scaled by the size of the pointer type.
   ```C
   unsigned int i = 261;
   int *p = &i;
   char *c = &i;
   ```
  * The code above is valid. Since pointers store memory addresses, it doesn't matter that in the third line, `c` is a `char *` even though `i` is an `unsigned int`.
  * Both `p` and `c` point to the first byte of the value for `i`.
  * If you do `p++`, `p` will increase by 4, since an `int` is 4 bytes.
  * If you do `c++`, `c` will increase by 1, since a `char` is 1 byte.
 ___

### Exercises
 * Do the following in a C program. It's going to get a little tricky, so do things one step at a time, compile, run and test frequently.
   1. Use the code snippet above to set up an `int` and 2 pointers.
   2. Print out the value of each pointer (this should be the memory address), and de-reference each pointer to print out the value each points to.
     * The output should look something like: `p: 0x7ffee3dbd938 p points to: 133`.
     * __Compile & run your program at this point.__
   3. Print out `i` in decimal and hex.
     * The `printf` formatting character for a hexadecimal int is: `%x`
     * The `printf` formatting character for an unsigned int is: `%u`
   4. Use `c` to print out each individual byte of `i`.
     * The `printf` formatting character for a single byte in hex is `%hhu` for unsigned decimal integer and `hhx` for an unsigned hex, (that is half of half of an integer).
   5. Use `c` to increment _each byte_ of `i` by 1. Print out the `i` in both hex and decimal after each modification. When done, print out each byte like in step 4. You may need to reset `c` so that it points to `i`, depending on how you wrote step 4 out.
   6. Perform the same operation as in step 5, except add 16 to each byte.
 * As you go through this, look at what's happening to each byte, and think about the level of control you have over the memory space used by your program. What values did you see for each individual byte? Can you make sense of them? Does the order make sense?
 * If you want to test things further try doing all the above with different kinds of values:
  * Try an `unsigned int` with a value greater that 2.1 billion.
  * Try a regular `int`.
