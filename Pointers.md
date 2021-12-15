# Pointers
## Defining Pointers
A *pointer* is a variable that contains the address of a variable. 
- Each pointer points to a secific data type (except a *pointer to void*). 
- Declare a pointer using type of variable it will point to, and a `*`.
- `int *p`; says `p` is the name of a variable that holds the address of an `int`.

## Operators
`&` address-of operator: returns address of whatever follows it.
`*` dereferencing operator: returns value being pointed to.

Examples:
```c
int x = 1;
int y = 2;

int *ip; /* declare ip, a pointer to int */
ip = &x; /* ip now "points to "x */
y = *ip; /* y is now 1*/
*ip = 0; /* x is now 0 */
```


Suppose `ip` points to integer `x`. Then `*ip` can be used anywhere that `x` makes sense:
```c
*ip = *ip + 10
```

Unary operators `&` and `*` bind more tightly than binary arithmetic ops. So, `y=*ip + 1` means take whatever `ip` points to, add one to it, then assign it to `y`.
This means `*ip += 1` or `++*ip` both increment what `ip` points to. (but parentheses are needed for `(*ip)++` since unary  operators associate from right to left).

### Assignment
`ptr1 = ptr2`; assignment works for pointers of the same type. Only the memory address in `ptr2` is copied. They will now reference the same memory location. Now, doing the operation `*ptr1 = 10` leads to `*ptr2 == 10` being true. 

### Comparison
`ptr == ptr2` and `ptr1 != ptr2` compare the addresses inside the pointer variables for equality (do they point to the same location?).
`ptr == NULL` will check if ptr is `0` (good initialization value to use). 
`ptr1 < ptr2` compares addresses.
- Useful if pointer variables reference memory in the same array for example (similar to comparing indicies). 

### Arithmetic and Arrays
Operators `+`, `-`, `+=`, `-=` can be used with other pointers or integers for the 2nd operand. 
Most often used on pointers to array because it doesn't add the actual number. It adds that number times how any bytes each element takes up based on the pointer base type. 
- For variable `int * p`, code `p+1` will add 4 bytes (`sizeof(int)`) to `p`'s address. So now, the pointer `p` will point to the second element in that array. 

For a declared array like `int a[10]`, `a` is "really" just a (non-modifiable) address that starts a block of memory.
- Writing `a` is the same thing as writing `&a[0]`.
- `a[3]` is a synonym for `*(a+3)` (offset three from pointer to start of array).
- `&a[3]` is a synonym for `a+3`.  

### Difference (subtraction)
`ptrdiff_t` is a predefined type in the library `stddef.h`. This is the resulting type when subtracting pointers (memory addresses). Equivalent to the `long` integer type. 
```c
int array[] = {3,4,5,6,7};
int * start = &array[0]; // first element address
int * end = &array[4]; // last element address
ptrdiff_t capacity = end - start + 1 // number of elements in array (5)
```

## Constants with Pointers
`const` means [constant](Basics%20of%20C.md#const.md) and can be used at different points in pointer type declarations, each with different meanings. 

To make a (mutable) pointer to a const (non-modifiable) data: `const int * iptr`. This prevents changing contents of the pointed to memory. 
-	Concept is similar to a `const int iray[]` where changing the contents, like `iray[0] = 10` is not allowed, but `iray = malloc(sizeof(int)` is allowed. 

To make a const (non-modifiable) pointer: `int * const iptr`. It prevents assignments to change (the address stored in) `iptr` or 	`iray`
-	Similar to `int iray[10]`; as a local variable. `iray = b;` is not allowed just as `iptr = &other` is not. 
-	If not a parameter, must set when declaring. 

To make a const `ptr` to const data: `const int * const iptr`. It doesn't allow changes to the pointer variable itself, or the memory it points to. 
- Similar to `const int iray[] = { 1,2,3 }`; as local variable.

Read declarations from right to left to get them correct.

## swap function example
```c
void swap (int *px, int *py) {
	int temp;
	temp = *px;
	*py = *px;
	*px = *temp;
}
```
The call in main now must be `swap(&a, &b)` since we need to send in the addresses of `a` and `b`. 
Swap function works because pointer arguments enable a function to access and modify values in the calling function.

# Pointers vs. C-Strings
Given these declarations:
```c
char str[] = "original";
char * str2;
```
- `strcpy(str2, str1);` will crash because memory for str2 was never allocated. This would work if you assign `malloc(strlen(str1)+1)` for str2.
- `str1+=3;` will not compile because we cannot change the address stored in a statically declared array variable. `*(str1+3)` creates a new pointer value, but it would work.
- `str2 = str1;` Makes str2 refer to the same block of memory as str1. Only copies the memory address stored in str1, and not the whole array. 