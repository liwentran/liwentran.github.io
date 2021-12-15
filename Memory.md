# Memory

## Execution Stack
Variables declared within a function get situated in memory within a structure called the program execution *stack* or *call stack*. When you run a program, this *execution stack* gets created. 
Each function call gets a new *stack frame*, also called *activation record*, put on top of ("pushed onto") the stack in memory; each frame has space for local variable values as well as parameters, and the values of arguments are copied into that frame.
As soon as the function returns, the stack frame will go to bay and all the variables will go away (since they live inside). 
![](Pasted%20image%2020210921205308.png)

To access a caller's stack frame, you need *pointers*.

### Arrays within a stack frame
Arrays, when passed through a function copies the *address* of the array, as this is more efficient. 
Since the calling function remains on stack while called function is executing, the address is still valid, so called function can access it.

### Limitations of Arrays Allocated within Stack Frames
When you try to declare an array in a function, it is local. When you return the statically-allocated array, it will not work. Calling function cannot access these arrays.

Segmentation fault error also occurs when allocating a very large array inside a function. Size of array is limited by size of stack frame. 

## Dynamic Allocation
Dynamic allocation is needed to get around the limitations of arrays allocated within a stack frame. 

Dynamically-allocated memory is located in a part of memory separate from the stack; it lives on "the heap". 
- This memory lives as long as we like (until the entire program ends).
- This memory is not subject to size limitations based on stack frame size.
- We can decide the size of a dynamically-allocated block of memory. 

To allocate memory, we use the command `malloc` (memory allocate) from `<stdlib.h>`. 
```c
// allocate space for one int in heap
int * ip = malloc(sizeof(int));
// check if allocation succeeded
if (ip == NULL) { /*output error message*/ }
// give the dynamically-allocated int an intial value
*ip = 0;
```

When usage of the dynamically-allocated variable is complete, deallocate it with the `free` command on the address of the memory on the heap:
```c
// notify system that we're through with heap int
free(ip);

// avoid accental attempt to use the pointer to access a released space
ip = NULL;
```
Deallocation does not need to occur in the same function where it was allocated, but some function *needs* to deallocate the block of memory. 

A tool to find memory usage mistakes is [valgrind](Tools.md#Valgrind).

### Dynamically-allocated arrays
To allocate an array with space for `n` items:
```c
int *a = malloc(sizeof(int) * n);
if (a == NULL) { /*output error message*/ }

// access an array item
a[0] = 0;
a[n-1] = 0;

// deallocate the entire array of size n:
free(a); 
a = NULL;
```

### Reallocate
`realloc` reallocates a given area of memory. Memory can be expanded or contracted, as long as the memory has previously been (dynamically) allocated. 
It can be done by
- expanding or contracting the existing area, if possible
- allocating a new memory block of new size bytes. There is a chance it changes the base address if there is another block right blocking the memory block you want to change. All the content will be moved automatically. 

On success, it will return the pointer to the beginning of newly allocated memory. On failure, it will return a null pointer. 

```c
int *ptr = malloc(sizeof(int)*100);
ptr = realloc(ptr, sizeof(int)*10000);
```

### callloc
Similar to `malloc`, but initializes all the bits to 0.
```c
int *pData = calloc (10, sizeof(int);
```
It takes two arguments: the number of elements you want and the base size. 

## Dynamically-allocated Two Dimensional Arrays
Method 1: 1D [array](Arrays%20and%20C%20Strings.md#Arrays) of items and "fake" two dimensions. 
```c
int *a = malloc(sizeof(int) * num_rows * num_cols); 
```
To access elements, convert `[row][col]` indexing to `[row * num_col + col]` and back. For example, `a[7]` means `a[2][1]` for `num_col == 3`.

Method 2: double (`**`) memory allocation
Use a 1D array of pointers to item arrays:
```c
int **a = malloc(sizeof(int*) * num_rows

for (int i =0; i < num_rows; i++) {
	a[i] = malloc(sizeof(int) * num_cols);
}

a[2][1] = 17 // this works

for (int i =0; i < num_rows; i++) {
	free(a[i]);
}
free(a); 
```
In this case, `a[i]` is of type int \*, an array of pointers to int. Each represents one row in the 2D array. 
### Non-uniform 2D arrays
It is possible for rows to be different sizes ("jagged"). Remember to free the memory for each row, and then the overarching array itself. All rows are different size so a parallel array to hold the length of each row is important. 
