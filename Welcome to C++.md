# Welcome to C++
## When to use?
C++ is not a "superset" of C; most C programs don't immediately work in C++. 
However, C++ tries to support as much as C as possible. 

Sometimes, C is the only option:
- "inherited" C code
- No C++ compiler is available for the target system
- Software must work closely with Linux kernel

Otherwise, a new project created today (especially if it was big or involved with many people) will use C++.


## What are the differences?
C++ is an object oriented programming language. 
- Classes (like Java)
- Templates (like Java generics)
- Standard Template Library (like `java.util`)
- More convenient text input & output

## Features and Concepts
- types: `int`, `char`, `float`, `double`, pointer types, and `bool` (C++ only)
- numeric representation & properties
- operators: assignment, arithmetic, relational, logical
- arrays, pointers `*` and `&`, pointer arithmetic.
- control structures: `if`/`else`, `switch`/`case`, `for`, `while`, `do`/`while`
- pass-by-value is still the default, but C++ gives the option to pass-by-address
- stack vs. heap, scope & lifetime
- `struct` works more similarly to classes.

The following tools still work:
- `git`
- `make`
- `gdb`
- `valgrind` 

## Hello World
hello_world.cpp:
```c++
#include <iostream>

using std::cout;
using std::end1;

int main() {
	cout << "Hello world!" << endl;
	return 0;
}
```
- `#include <iostream>` links the [library](Welcome%20to%20C++.md#C%20Libraries) for input and output. 
- `using std::cout;` and `using std:endl;` these two belong to `std` [namespace](Welcome%20to%20C++.md#Namespaces).
- `cout` displays something on the [standard output](Welcome%20to%20C++.md#I%20O).
- Source files have extension `.cpp`.

### Compiling 

```sh
g++ -std=c++11 -pedantic -Wall -Wextra -c hello_world.cpp
```
- `g++` is the standard compiler that we will use for this class. 
- `-c` compiles, but does not link. Gives the object code.

```sh
g++ hello_world.o -o hello_world
```
- Link and create an executable. 

```sh
./hello_world
```
- Execute
- Feed an input at the same time as executing by using `echo INPUT | ./cpp_io`


## C++ Libraries

Include library headers with `<` angle brackets `>`. Omit the trailing `.h` for c++ headers:

```c++
#include <iostream>
```
`iostream` is the main C++ library for [input and output](Welcome%20to%20C++.md#I%20O) (like collecting user input and displaying to standard out).


User-defined headers use `"` quotes `"` and end with `.h` as usual:
```c++
#include "linked_list.h"
```

Use familar C headers like `assert.h`, `math.h`, `ctype.h`, `stdlib.h` by dropping the `.h` and adding `c` at the beginning.

```c++
#include <cassert> // the assert.h header from C
```

## Namespaces
```c++
using std::cout;
using std::endl;
```
Think of namespaces as modules or packages. They are used to create structure. 
- In C, when two things have the same name, we get errors (from compiler or linker) and confusing situations ("shadowing")
- In C++, items with the same name can safely be placed in distinct "namespaces". 

### Using
`using` gets rid of the need to write fully qualified name (`std::cout`) every time by including it. Otherwise, you would would have to write the fully qualified name each time: `std::cout << "Hello World" << std:endl;` instead of `cout << "Hello World" << endl;`
- `::` is a scope operator, it means "belong to".

### Rules
Do not ever use `using` in a header file. It affects all source files that include that header, even indirectly, which leads to name conflicts.
- Only use in source `.cpp` files. 
- Use fully qualified names (e.g. `std::cout`) in header files.

Do not use `using namespace std;` because too broad.
- This is a catchy-all way to include everything in the `std` namespace, which causes confusion due to accidental name conflicts. 

## I/O
```c++
cout << "Hello world!" << endl;
```
`cout` prints to the standard output stream (like `stdout` in C).

`endl` is the new line character. 

`<<` is the *insert output* which allows you to insert something into the out put.  

There are no format specifier (`%d`, `%s`, etc.). Items that need to be printed are arranged in printing order, which is easier to read and understand. However, if you still want to use it, it does work after including `<cstdio>`. 

### Chaining
In the above example, we send two things to `cout`, this is called *chaining*. The insert operator joins all the items to write in a "chain". 
The leftmost item in the chain is the stream being written to. 
```c++
cout << "We have " << inventory << " " << item << "s left." << endl;
```
`inventory` and `item` are variables. 

### Operator Overloading
`<<` usually does bitwise left-shift; but if operand on the left is a C++ stream (`cout`), `<<` is the insert operator. Shifting only applies to numbers. 
More on this later. 

### User input
```c++
string name;
cin >> name;
```
- `>>` is the extract operator. Collects from standard input and stores it into the variable provided. 
- `cin` is mapped to standard input. It reads one whitespace-delimited token from standard input and places the result in the string `name`. 
- Note: both are part of standard namespace: `using std::cin` and `using std::string`

 If you input an entire sentence, it will still read one token at a time (word by word per iteration). This code will store the smallest word in an inputted sentence and print it out. 
 ```c++
 string word, smallest; 
 while (cin >> word) {
 	if(smallest.empty() || word < smallest) {
		samllest = word;
	}
 }
 count << smallest < endl; 
 ```
 - Note: relational operators work with strings. (operators were overloaded). 

```c++
cin.get(ch)
```
- Reads one character from the standard input