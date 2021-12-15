# Basics of C
## Printing
`printf` can output a literal string and also allows for formatting printing of values, using placeholders in the fomrat string:
```c
printf("There are %d students in class.", 36);
```
Placeholders begin with '`%`' and then may contain additional format information. The actual values corresponding to place holders are listed afte rthe format string (`36` in this example).
- Generate a literal `%` character by specifying two `%` characters in the format string. 

### Data Type Placeholders
Some common data type placeholders to use after the `%`: 
- `d` - decimal (integer type)
- `ld` - long int
- `u` - unsigned (integer type that dis allows negatives)
- `lu` - for long unsigned
- `f` - floating point 
- `e` - scientific notation
- `lf` - for double
- `c` - character
- `s` - string

## Variables
```c
int num_students;
```
declares a variable with *type*  of `int` and *name* of `num_studnets`.
A variable has a *value* that may change through the program's lifetime. It's value can be printed with `printf`.

A two-word variable in C is often written using underscores rather than camel case (e.g., `numStudents`).

## Types
Try to use the smallest data type. See all the data types [here](https://en.wikipedia.org/wiki/C_data_types).

Integer types
- `int`: signed integer, stored in 32 bits.
- `unsigned`: unsigned integer. Always considered positive.
- `long`: signed integer with significantly greater capacity than a
plain int

Floating-point (decimal) types
- `float`: single-precision floating point number. 4 bytes.
- `double`: double-precision floating point number. 8 bytes. Can store more decimal digits. 

Character types
- `char`: holds a 1-byte character, `A`, `B`, `$`, ... They are stored in their unicode value.
- Chars must be in single quotes. Double quotes are only for strings. 
- `chars` are basically integers, so they work for logic statements. This is valid: `char digit = '4' - 1`. ASCII standard governs the mapping between characters and integers. Use `(int)char_variable` to explicitly convert. 
- The C character library `#include <ctype.h>` contains a bunch of [useful functions](https://www.tutorialspoint.com/c_standard_library/ctype_h.htm) we can apply to character values. Boolean functions include `isalpha`, `isdigit`, `islower`, `isspace`, etc that return non-zero for true and zero for false. Conversion functions include `tolower` and `toupper`.  

Boolean
- `#inlcude <stdbool.h` to use this.
- `bool`: value can be `true` or `false`
- Integer types can function as `bools`, where `0` means `false` and non-0 means true. 
## Assignment
```c
num_students = 32
```
`=` Is the *assignment operator*, which modifies a variable's value.

It's good practice to declare and assign at the same time:
```c
int num_students = 32
```
This prevents "undefined" values (variable that has been declared but not yet assigned). "Undefined" values can cause mysterious fails.

## Operators
```c
3 + 4
```

`3` and `4` are "operands" and *constants* (not variables) and `+` is the "operator".

Arithmetic operators include `+` (addition), `-` (subtraction), `*` (multiplication), `/` (division), and `%` (remainder).
- Beware of integer division: `7 / 2` yields `3`, not `3.5`

### Operator Precedence
Precedence can be found [here](https://en.cppreference.com/w/c/language/operator_precedence). 
Use parentheses when in doubt.

## Const
Put `const` before the type to say the variable to which it is applied cannot be modified.

To make a variable non-modifiable: 
```c
const int base = 32;
```
- If applied to a local variable, it must be initialized when declared.
- If applied to a parameter variable, it cannot be changed within the function. You can pass a non-`const` variable to a `const` parameter, but you cannot pass a `const` variable to a non-`const` parameter.

## Formatted input with `scanf`
```c
// scanf_d.c:
int i;
printf("Please enter an integer: ");
scanf("%d", &i);
printf("The value you entered is %d", i);
```

The `scanf` function works similarly to `printf` for reading formatted input. 
Use a format string (`%d`) followed by the memory location(s) (`i`) we are reading into. Use the `&` sign before the variable name. 
- Match the format string to the [type of value](Basics%20of%20C.md#Data%20Type%20Placeholders) you want to collect. The memory location should be able to accomodate this type. 

The return value of `scanf` is the number of input items assigned.
- Zero typically indicates that the input was available but invalid for the specific type.
- EOF (`-1`) indicates that no input was available.