# Lifetime and Scope

## Lifetime
*Lifetime* of a variable is the period of time during which the value exists in memory.

## Scope
*Scope* of a variable is the region of code in which the variable name is usable.

A variable in scope may be temporarily "hidden" when an inner scope declare a variable with the same name.
```c
int i = 12;	// a variable named i
printf("i before loop: %d	", i);
for (int i = 0; i < 1; i++) { 	// a new variable named i
	printf("i inside loop: %d	");
}
printf("i after loop: %d	", i);	// the old i
```
Output:
```
i before loop: 12	i inside loop: 0	i after loop: 12
```
The variable foo takes precedent. 

## Types of Variables
**Local ("stack") variables** are alive from the point of declaration until end of block in which declared. 
- They are automatically created when that function is entered, and destroyed when that function ends. 
- Local variables go out of scope during calls to other functions because it will be in a different stack frame. (e.g., you cannot access a variable in main if you are in a different function). 

**Static variables** (declared using the `static` keyword) have similar scope to local variables, but have a longer lifetime. 
- Automatically created and *initialized to zero(!)*, but not destroyed at the end of block of code. They persist, so that the next time same block is executed, they come back into scope with the same value they had before. 

**Global variables** (declared outside any function; right under the headers) are automatically created at program start and *initialized to zero(!)*. 
- They have scope from point of declaration to the end of program.
- Can be accessed by any function.
- Can be accessed by functions in other files (after brought into scope using `extern <type> <name>` in that file). 
- Beware of global variables because they make debugging much harder. It is hard to track which function might have changed a global variable's value. Since they cross boundaries between program modules, it undoes benefits like readability, testability, and reusability. 
	- Values should be conveyed via parameter passing and return values.
	
### Where are they stored?
Local variables are stored in a region of memory known as the [stack](Memory.md#Execution%20Stack). 
- Stack frames are added/removed as functions get called and then return.

Both static and global variables live in a region of memory known as the data segment. 
- Data segment is allocated when program begins, freed when program exits.

Dynamically-allocated memory lives in a third region of memory, called the heap.
- The user is responsible for allocating and freeing memory in the heap. 