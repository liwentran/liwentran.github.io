# I/O
## Standard Streams
`printf`, `scanf` only works with `stdin`/`stdout`. They use the *standard stream*.
 
They don't have to be closed or opened; C handles that You can refer to them by these names, defined in `stdio.h`:
 - `stdin`
 - `stdout`
- `stderr`

For example, `fprintf` can write to `stdout` like `printf`:
```c
fprintf(stdout, "Hello World\n");
```
## C File I/O
`fprintf`, `fscanf` works with any files. Good for big inputs and outputs.
### fopen
```c
fopen("output.txt", "w");
```
Use relative file path for the first parameter.
The second parameter indicates the modes, which are:
- `"w"` opens file for writing
- `"r"`: reading
- `"r+"`: open for reading and writing. 
- `"w+"`: open file for reading & writing.
 
Note: `"r"` and `"w"` are common. `"w"` and `"w+"` causes the named file to be overwritten if it already exists. 

`fopen` returns a `FILE*`, a pointer to the `FILE struct`. Returns `NULL` and crashes if `fopen` failed. 
- `NULL` is a special pointer value, usually equal to `0`, and is a common way to indicate failure for functions with pointer return type. 
```c
FILE* input = fopen("numbers.txt", "r");

if (input == NULL) {
	printf("Error: could not open input file\n");
	return 1; // indicate error 
}
```
### fscanf
```c
fscanf(input, "%d%d", &destination1, &destination2) 
```
- reads each line in the file named `input`.
- `scanf` returns the number of input collected. Do `while (numCollected ==2)` to make a loop that keeps collecting two inputs from each line. Then, check if `(numCollected != EOF)` because it would indicate that the program could not parse line instead of reaching the end of file.

### Other Functions
- `feof(fileptr)` returns non-zero if we've already read past the end of the file. 
	- Starts reading from the beginning of the file, and as you start reading, the cursor moves. 
- `ferror(fileptr)` returns non-zero if file is in an error state,
	- e.g. if we've opened file for writing but then attempt a read.
- `rewind(fileptr)` returns `fileptr` to beginning of file. 
- `fclose(input)` closes input file.

# Assertions
```c
assert(boolean expression);
```

Assertion statements help catch bugs as close to the source as possible. 
- `#include<assert.h>` is required to use.
- `boolean expression` is an expression that *should be true* if everything is okay. 
- If it's false, program immediately exits with an error message indication failed assertion. 
- Create *test cases* using `assert` to make sure certain states exists. 

They make your assumptions clear:
```c
int sum = a*a +b*b;
assert (sum >= 0);
```
We should use assert when we are verifying something about the logic of your program (checking for something that implies your program is incorrect). Use if statements to check the external environment and for bad user input. 
- For example, when using `fopen` to open a file, we use  `if(input = NULL)` instead of an `assert (input != NULL)` because if there is a problem, it would be the fault of the file (missing or corrupt), and not the program. 