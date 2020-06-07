# Bit Off More Than I Could Chew.
## 9/18

### Administrative Stuff
 * I received some feedback that yesterday's lesson, and exercises, were on the confusing side. So today we're going to take a step back and hopefully provide some clarity.
 * Also, all these lessons are up on github, so for example, when I ask you to de-reference a pointer, if you don't remember how to do that, just look at the previous lesson for an example. I'm probably not going to repeat myself too much given that all the notes are easy to retrieve.
---

### Bits & Bytes
 * All digital data is _binary_, broken up into series' of 1s and 0s.
 * Physically, this data can take many forms, electronic (high voltage | low voltage), optical (light on | light off), magnetic (+ | - magnetic charge) and so on.
 * A single 1 or 0 is a __bit__, a unit of digital data.
 * 8 bits make a __byte__.
   * Why 8? - Some people thought that was a good number. It used to be 4.
 * If you have a music file that is 5 MB (megabytes) large, that means it takes 5 million bytes, or 40 million bits to be represented digitally. That's 40 million individual 1s and 0s in whatever physical form it may be.
---

### Computer Memory Basics
 * In order to get all this pointer stuff down, we have to be cool with understanding computer memory. So let's do that.
 * In general, memory is the term used to describe the computer part that contains any active data. Active data includes things like:
   * All open applications, even ones running in the background.
   * All open files.
   * Operating system.
   * Background processes.
 * Let's say a computer has 4 gigabytes of memory, that means it can handle 4 billion bytes of data open at once.
 * The important distinction to be made is between _memory_ and _storage_.
   * _Storage_ refers to data stored on disk (Hard Drive, SSD, Flash Drive, Floppy Disk...).
   * Storage is where data gets saved for the long term. At any given time, most computers will have a lot more data in storage than in memory.
   * For example, you might have the entire [Pearl Jam](https://en.wikipedia.org/wiki/Pearl_Jam) discography stored on your hard drive, but you can only listen to one song at a time, so the song you're currenlty listening to would be the only data in memory out of all the other songs in storage.
 * Memory is much faster to access than storage, which is why it is used. THe downside is that memory is _volitile_, meaning it requires power to retain data (imagine losing everything when you shut your compuer off), and it's much more expensive than storage.
 * The most common form of memory is RAM (Random Access Memory). The more RAM you have, the more data you can hape open at once.
   * Computers can use a concept called _virtual memory_, which will allocate unused disk space for memory purposes in the event that your RAM is full.
 * When you open a program/file (in the *nix world, everthing is a file), the file is __copied__ from storage into memory. Saving a file reverses this process, taking the changes you've made from memory and copying them into storage.
---

### Interacting with Memory in your Programs
 * Just like any other program, when a program you write is run, it takes up memory space.
 * Every variable and function you write gets turned into bits which takes up memory space when run.
 * In this class, when we talk about the memory usage of a program, we will mostly be talking about variables.
 * For example, when you declare an `int`, that means your program will request 4 bytes of memory to store a value. See [lesson 02](02_variables.md) for the chart of types and sizes.
 * Previously, I provided a link to the [wikipedia entry on endianness](https://en.wikipedia.org/wiki/Endianness), but I'll go into more detail here.
   * Forgetting about computer data for a moment, think baout normal decimal numbers. In the number 2,354 we would say 2 is the most significant digit, because that 2 represents 2 thousand, the largest value of any digit in that number.
   * Generally, we write decimal numbers left-->right from most-->least significant.
   * Endianness is a similar concept, except instead of thinking of the significance of digits, we look at the significance of __bytes__.
     * Consider the value `261`. In binary, that would be: `100000101`, which is a 9 bit number.
     * To store `261` in an `int`, C will use 4 bytes, so it would really look more like this:
       * `00000000` `00000000` `00000001` `00000101`
     * Think about the significance of bytes in the same way you think about the significance of digits. In the above representation, the most significant byte comes first. Since we only need 9 bits (which is spread over 2 bytes) to represent `261`, the first two bytes are all `0`. The third byte, `00000001`, represents the number `256`.
     * Systems that use this representation are called __big endian__.
     * Other systems use the reverse order, going from least significant to most significant byte. These are called __little endian__.
     * `261` in __little endian__ format would be:
       * `00000101` `00000001` `00000000` `00000000`
       * Notice that the indicidual bytes are in most->least significant bit order, but the order of the bytes is reversed.
     * Another example, `2,151,686,160`
       * Big endian: `10000000` `01000000` `00100000` `00010000`
       * Little endian: `00010000` `00100000` `01000000` `10000000`
 * Back to the whole pointer thing, consider the following C snippet:
   ```C
   unsigned int i = 2151686160;
   int *ip = &i;
   char *cp = &i;
   ```
   * `ip` and `cp` will store the address of the first byte used to store `i`. Depending on the _endianness_ of the system, that byte will either be `10000000` (big) or `00010000` (little).
   * Let's just say that the first byte is located at memory address `3000` (using small number for ease of discussion)
   * If you perform `ip++` and `cp++`, each pointer will be incremented by 1, but due to pointer arithmetic, `ip` will increase to `3004` and `cp` will increase to `3001`. In essence, `ip` would move one `int` forward in memory, while `cp` only moves one byte forward.
---

### Printing Values in C
 * `printf` provides different ways of printing out values.
 * Remember that no matter how you write a number in your code, it is stored in memory in binary, so as far as `printf` is concerned, even printing out a value in decimal (base 10), requires translating the stored data.
 * There is no such thing as a "native" hexidecimal or decimal number. You write them in your code in some way, and they turn into binary when the program is compiled.
 * So `printf` takes the binary data, and displays it in a particular way based on the formatting character(s) provided.
 * `%d` : print a value as a signed decimal `int`.
 * `%u` : print a value as a decimal `unsigned int`.
 * `%o` : print a value as an octal number.
 * `%x` : print a value as a hexidecimal number.
   * `%o` and `%x` will always treat the value as if it were unsigned.
   * You can print a value out with `%u` or `%d` regardless of how it is declared, that doesn't mean it will make sense, just that `printf` will convert the value accordingly.
 * `h` : modify the printed value to look at 2 bytes instead of 4.
 * `hh` : modify the printed value to look at 1 byte.
 * `h` and `hh` can modify `u`, `d`, `o` or `x`.
 * The code snippet below displays these options:
   ```C
   unsigned int q = 2151686160;
   printf("%%d: %d\n", q);
   printf("%%u: %u\n", q);
   printf("%%o: %o\n", q);
   printf("%%x: %x\n", q);
   printf("%%hhx: %hhx\n", q);
   printf("%%hhu: %hhu\n", q);
   ```
 * When run, this prints (on my computer):
   ```
   %d: -2143281136
   %u: 2151686160
   %o: 20020020020
   %x: 80402010
   %hhx: 10
   %hhu: 16
   ```
 * Things to notice:
   * `%d` is not the actual value we used, this has to do with how negative numbers are represented.
   * `%hhx` and `%hhu` print the first byte of the value. Based on that, you can tell the endianness of the system the program is run on (it is possible you get a different result from my example).
---

### Where to go from here
 * Hopefully this clears up some things.
 * Go back to the exercises from yesterday. My goal was to have you tease out the way numbers are stored in memory. Pointers give you the ability to work your way through the memory of your program one byte at a time. You can tell a lot about how values are prepresented by examinding memory in this manner.
 * If you got through all the exercises from yesterday, here are some questions you should try to answer through careful examination of the memory. FOr some of these, it might help to use variables that are smaller than an `int`, since 32 bits is a lot to go through.
   * Is the system big or little endian?
   * Can you figure out how negative integers are represented?
   * What happens when you go over/under the limit for a particular data type?
   * What can you find out about floating point numbers? (this is tricky)
