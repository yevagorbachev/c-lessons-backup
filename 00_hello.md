## C is for ~cookie~ C!

### Administrative Stuff
 * JonAlf Dyrland-Weaver (me), will be out at the start of the school year on parental leave. I should return 6 weeks from __8/22__
 * Until I return, class notes will be provided in this repo, numbered sequentially.
 * Assignments (as well as other importan pieces of class information) will be posted on the class website: http://www.stuycs.org/courses/mks65/dw
 * I will use a mailling list to send out important information, and we will use a google group as our class QAF (Question and Answer Forum, pronounced quaff). The QAF will be heavily utilized to provide class discussion.
 * All assignments will be collected using GitHub, you must have (or create, it's free) a GitHub account for this class.
 * I will be experimenting with GitHub classroom to create assignments, it _should_ streamline the assignment process, but there may be some kinks to work out intially, we shall see.
 * You can contact me via email: dw@stuy.edu. Note that I may not be quick to respond during the parental leave period.
 ---
 
 Today I'm just going to cover some basic information about C. Hopefully you will get a feel for the place of C in the pantheon of programming languages, as well as a bit of understanding as to its importance. Tomorrow we will dive into writting, running and compiling C programs.

### C Basic info
* C is a producural programming language developed in the early 1970s by Dennis Ritchie at Bell labs.
* Unlike java, there are no _objects_, instead, the basic pieces of C programs are procedures/functions.
* C works more like python, write functions and use them, though it is a compiled language.
* C sytax is the same as java syntax (lines end with ; , {} for control structures and functions, basic assignment and boolean operators ...), though to be more corrext, java sytax is C syntax. The developers of java (early 90's) decided to use C syntax so it was easier for programmers to adopt the new language.
* C does not hava a virtual machine like java, C code must be compiled for a specific __platform__ (processor type + operating system). Therefore compiled C files cannot work on different computers, unlike java .class files.
 * C was designed to write programs that run _fast_, like, real _fast_. A program written in raw binary (machine code), would run the fastest, as no interpretation would be required. But humans don't think in binary, so the next step up is Assembly Code, which uses commands like `mov` and `dec` instead of binary. It's better to read than binary, but not by much. C is a much more structured and human-readable language, but compiled C code retains the executaion speed of assembly. 
 
### Is C important in 2019?
 * C is over 40 years old, back then, computers wer the size of closets, hard drives held ~5MB, RAM was ~8KB, processor speeds chugged along at 1MHz. Surely, we've got better languages now...
 * C programs are still the fastest (or amongst the fastest depending on the analysis). Here's [one such analysis](https://jaxenter.com/energy-efficient-programming-languages-137264.html), though you can find many others.
 * C is the precursor to many newer languages including C++ and Objective-C.
 * Due to it's speed, stability and longevity, C is still one of [the most popular programming languages](https://www.tiobe.com/tiobe-index/).
 * Compiled C programs also tend to be very small, making it ideal to use for small devices (i.e. the Internet Of Things).
 ---
 
__Assignment__ 
 * Please fill out the following survey: https://forms.gle/TVpGMyKN3UGqtHC88
