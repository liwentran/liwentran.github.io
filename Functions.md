# Functions
`printf`, `scanf`, `isalpha`, ... are all functions. 

Functions must be called to be executed.

> “Experience has shown that the best way to develop and maintain a large program is to construct it from smaller pieces or modules, each of which is more manageable than the original program.”

Factoring your code into functions helps...
- keep concentration on smaller problems, one at a time. 
- makes code readable
- with testing because you can test *functions* one by one and are easy to write. 
- with collaboration.

You know you need to put code in a new function when...
- the code has a clear distinct goal.
- the number of variables used in the snippet is not large. 
- the code has a single result.

## Defining Functions
Function definition should appear before it is used.  
- "Definition" means full implementation of something.
- "Declaration" is just declaring that there's going to be a function with this name, return type, property, etc. 

```c
int foo(char c, int i) {
	return i;
 }
```
- `int` is the *return* type.
- `foo` is the *name*.
- `(char c, int i)` is the *parameter list*.
- `char c` and `int i` are *parameters*. Calls to function match arguments with these.
- Everything inside `{` curly braces `}` is the body.

A function return nothing has return type `void`, and does not need a return statement. 

Use empty parameter list `()` or `(void)` if the function does not have parameters. 

## Declaring Functions
We can "declare" a function before the function that calls it, then fully define it later (after `main()`), after calling function's definition.
```c
flaot func1 (int x, float y); // declaration
```
- Semicolon after parameter list
- Declaration appears before the function definition containing first call to function. 
- A function declaration is also known as a *funtion prototype*.

## Communication Between Functions
Functions communicate with function parameters and/or function return values. 

External (global) variables are another option; though use of these is discouraged. 

## Parameter passing
Argument values in C are passed by values.
- The function is given argument values in temporary variables (not original). You pass a copy of the value so you cannot directly modify an argument variable back in the calling function. This is called "pass by value."

As soon you return from the function, all the local things will go away, such as the parameters. This means, you cannot return local arrays. 


### Passing Arrays
[[Arrays and C Strings#]] are *not* passed by value. Instead, passing array amounts to passing a *pointer to its first element* because  copying would be excessive. 
- A [pointers](Pointers.md#Defining%20Pointers) is a variable which holds an address. 
- It "decays" into a pointer because it loses information about the boundaries of the array. 

Now, the callee *can modify* the array. 
Example:
```c
// multiply each array element by factor, modifying the array.
void scale_array (float arr[], int len, float factor) {
	for (int i = 0; i < len; i++) {
		arr[i] *= factor;
	}
}
	
```

When an array parameter *should not* be modified by the function, add `const` before the type. Compiler gives an error if you try to modify a `const` variable because it is `read-only`.

## Returning an Array
The return type is the array's base type with `*` added (a pointer). 

For now, we can pass in an empty array to fill. Instead of returning a local array, caller should pass in "destination" array to modify.

# Command-Line Arguments
When you tyep `mkdir cs220` you're running a program called `mkdir` and passing it a single *command-line argument*, `cs220`.

C programs can take arguments similar to this way, but you have to declare your `main` function in a special way: 
```c
int main(int argc, char* argv[]) {
...
}
```
- `int argc` is a parameter that equals the number of command-line argument. 
- `char* argv[]` is the second parameter that takes in an array of strings. Each element in the array is the string and is a command line argument. Also seen as `char argv[][]` or `**argv`
- E.g. `./a.out rosebud` is actually `argc` value of `2` because `./a.out` counts as one argument. `argv[0] = ./a.out` and `argv[1] = rosebud`. 


# Math Functions
`#include math.h` and compile with `-lm` option (includes the math library when *linking* to the `gcc` command to get access to: 
- `sqrt(x)`: square root
- `pow(x, y)`: xy  
- `exp(x)`: ex  
- `log(x)`: natural log
- `log10(x)`: log base 10
- `ceil(x)` / `floor(x)`: round up / down to nearest integer
- `sin(x)`: sine (other trigonometric functions available)

`x` and `y` arguments have a type `double`. Passing `int` is also OK. 
- Argument type promotion: `int` -> `float` -> `double`