# How to Write Functioning Code
### 9/23
---

### Do Now
 * Share your programs that test the various string functions with your neighbor(s).
 * When discussing, talk about the follwoing things:
   * Were you confused by any of the functions?
   * Did you have trouble demonstrating any of them?
   * What happens if you pass strings into these functions that were not properly `NULL` terminated?
---

### C Functions
 * All functions in C are _pass by value_.
   * This means that the arguments are __copied__ into new variables when the function is called.
   * As a result, normal values are not modified when passed into a funtion. Consider this function to swap two values:
     ```C
     void swap(int a, int b) {
        int t = a;
        a = b;
        b = t;
     }

     //later on...
     int x = 10;
     int y = 5;
     swap(x, y);
     ```
   * In this example, when `swap` is run on `x` and `y`, `a` and `b` are created. The function swaps the values of `a` and `b`, but once the function finishes, it is popped off the call stack, and `a` and `b` are gone. `x` and `y` are left unchanged.
 * This is where pointers come in handy. If you pass a pointer to a memory address, then you can modify the value it points to. Look at this modified version of swap.
     ```C
     void swap(int *a, int *b) {
        int t = *a;
        *a = *b;
        *b = t;
     }

     //later on...
     int x = 10;
     int y = 5;
     swap(&x, &y);
     ```
   * Now that `swap` takes pointers, we can de-reference the parameters to get at the values pointed to. When the function is colled, `a` and `b` become copies of the _adrresses_ of `x` and `y`, so when `swap` finishes, the values will actaully be swapped.
 * Passing pointers as arguments is actually waht happens in java when object variables are used, you may recall the phrase _pass by reference_, all that means is pass by value, but the value being passed is a memory address.
 * When you pass an array as a argument to a function, the entire array is _not_ copied. Since array variables are pointers, all arrays are treated as regular pointers when passed into a function. The following function headers are equivalent:
   * `void arr_func( int arr[]);`
   * `void point_func( int *arr);`
   * It is generally preferred to use the second option, since it makes clear that the parameter is a normal pointer. It is possible to use the first option and think that something special is going on due to the array notation (but nothing is).
---

### Exercises
Hint: For problems 1 and 2, you might find it helpful to add an extra parameter.
 1. Write a function that takes an array of `int` values as a parameter and returns the average of those values.
 2. Write a function that takes 2 arrays of equal size as paramters (you can chose the type). The function should copy the values of the first array into the second.
 3. Write a function that takes a string as a parameter and returns its length. When calculating the length of a string, do not include the terminating `NULL` in the result. (You should not use any extra parameters here)
