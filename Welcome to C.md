# Welcome to C
## Typical C Workflow
1. Edit files with emacs or vim. 
2. Compile using a GNU C compier (abbreviated as "gcc") to compile, link, and create executable. 
3. Run the executable file.

It's better to code incrementally as you will have a better time debugging. 

## Compiling
Step 1: Preprocessor
- Brings together all the code that belongs together
- The preprocessor quickly scans your code and processes any directives that start with `#`, such as `#include` or `#define`
	- Checks that the library exists.

Step 2: Compiler
- Turns human-readable *source code* into *object code* (executable code with the extension `.o`)
	- Change the name of the output (executable) file from the default *a.out* using the `-o` output flag. 
- Might yield warnings and errors if your code has mistakes that are "visible" to the compiler.

Step 3: Linker
- Brings all relevant *object code* (the `.o` files) into a single executable file (default name of `a.out`).
- Might yield warnings and errors if relevant code is missing, there's a naming conflict, etc. 
- We need full implementation of the function. 

## Understanding Hello World program
``` c
// hello_world.c:
#include<stdio.h>

// Print "Hello, world!" followed by a newline and exit
int main(void) {
	printf("Hello, world!\n");
	return 0;
}
```
- The file is named `hello_world.c`. C files have the `.c` extension. 
- `#include` is a preprocessor directive, similar to Java `import`. Omitting `#include <stdio.h>` results in an error. 
	- `stdio` is standard.io and `.h` is an extension that is short for "header". Header functions are used to declare things. 
- `main` is the function. Every program has exactly one `main`. It is the entry point and where the execution starts.
- `int` is the function's return type.
- `main(void)` says that `main` takes no parameters (inputs).
- `printf` prints a string to "standard out" (the terminal). This function is defined in the standard.io library (must include `<stdio.h>`). 
- `\n` is a string that denotes the newline chracter.
- `return 0` means "program" completed with no errors. `return 1` (or any non-zero value) would indicate an error.
- `// Print...` Explanatory comments before functions are good practice. Ignored by the compiler
### Compilation and Execution
To compile hello_world.c and link to give executable file:
```
gcc -std=c99 -Wall -Wextra -pedantic hello_world.c
```
- The flags and switches are the parts that start with a `-`. Each switch has meaning. 
	- `-std=c99` sets the standards to c99 made in 1999 (a popular standard still used today).
	-  The other three switches makes sure we get full verbose feedback from the compiler.
		- If you get an error feedback, your code won't even compile. Warnings indicate potential problem but will continue to compile. 

To run executable file named `a.out`:
```
./a.out
```
- `./` refers to something inside the current directory.
- `a.out` executes `a.out` from the current directory. 

## Multiple Copies of Code
To "snapshot" code is making a copy. Frequent "snapshots" is bad because it's hard to remember the relationship of copies, wastes space, and is difficult for team members to track the latest version of each file.

Git uses a *repository* ("repo") to store all versions of all project files. A repo (master/origin) can be *local* (on your computer) or *remote* (e.g., on bitbucket.org or github.com).