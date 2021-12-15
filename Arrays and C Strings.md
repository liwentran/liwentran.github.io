# Arrays
An *array* variable is a *collection* of elements laid out consecutively in memory. All elements have the same declared type. Individual elements are accessed with the `[]` notation must come after the variable name.
The actual value of an array variable is a memory address in C. 

This is the declaration of an array that can hold 12 integer values:
```c
int c[12]
```
The first element can be accessed with `c[0]` and the last element is always one less than the size of the array (i.e., `c[11]`).
Assign a value to an element with `c[0]=7`.

If you try to access your array before initializing, then do not know what value the elements will have and you will get warnings. 

## Initializing Arrays
With a `for` loop:
```c
int c[12]; // elements undefined
for (int i = 0; i < 12; i++) {
	c[i] = i; // initialize with value matching index number
}
```

With literal values by using values separated by commas within `{ ... }`. Array size can be omitted when initializing with `{ ... }`. 
```c
int c[5] = {2, 4, 6, 8, 10};

c[ ] = {2, 4, 6, 8} // no size
```

## Whole Array Operations (NOT)
- There is no "slicing" in C. (E.g., can't access several elements using `c[1:4]`).
- Cannot print (`printf("%a", c)`) or read (`scanf("%a", c)`) a entire entire array (except for char arrays).

# Strings
Strings are a sequence of characters handled as a unit; not a separate type. It is an array of characters with the final character equal to the "null character", `\0`, also called the "null terminator," and has the first character on the ASCII table with a value of 0. 

Two declarations of string. The first declaration shows a string is like an [array](#Arrays). The second uses an array with the final character equal to the "null character” and both first and second strings are *null-terminated* and are arrays of size 7. The third declaration shows a string is like a *pointer*.
```c
char day[] = "monday";

// same as
char day[] = {'m', 'o', 'n', 'd', 'a', 'y', '\0'}

//alteratively
const char *day_ptr "monday";


```

## String Character Access

*Indexing*, or accessing elements of the string utilizes *square bracket* notation.

```c
cnst char str[] = "hello";
print("%c %c \n", str[1], str[2]) // prints "e l"
```

## Printing Strings

Strings are an array of null-terminated (`\n`) characters. Null termination is used to indicate where the string ends, so it will only print chars up to the (first) `\n`.

```c
printf("%s", s);
```

## String Functions

Size-related functions that return an unsigned long (`%lu` format string). 
- `strlen` function returns number of chars before `\n`. (best way to find length of a given variable). From the `#inlude <string.h>` library.
- `sizeof` function returns amount of space occupied by a variable; the total # of bytes. 
  - `sizeof(type_name)` like `int` it tells you how many bytes an integer type is. `sizeof(array_var)` also tells you is declared size. 
  - If you had an array named `ra` of 5 integers, `sizeof(ra) / sizeof(int)` would tell you the size of the given array. Works with any type. 

`#include<string.h>` includes helpful string functions:

- `strcmp(s1, s2)` compares two strings according to character ASCII values. 
  - Negative value: `s1` before `s2`, Zero: `s1` and `s2` are equal. Positive: `s1` after `s2`.
- `strcpy(s1, s2)` copy effect is like `s1 = s2` as long as `s1` is declared with a sufficient size to fit `s2`.
- `strcat(s1, s2)` concatenate effect is like `s1 = s1 + s2` as long as `s1` is declared with a sufficient size. 
- See more: `strncpy`, `strncat`, `strtok`, and [others](https://www.cplusplus.com/reference/cstring/). 

## String Operations (NOT)
- There is no concatenation operator `+`. 
- No assignment `=` between strings declared as arrays. You cannot do a whole assignment into an array because it is a fixed memory address. 
- Assignment is allowed between strings declared as pointers.

