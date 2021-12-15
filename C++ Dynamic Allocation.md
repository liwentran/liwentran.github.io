# C++ Dynamic Memory Allocation
`new` and `delete` are essentially the C++ versions of [`malloc`](Memory.md#Dynamic%20Allocation) $and `free`. The difference is that `new` also calls the appropriate constructor if used on a class type along with allocating the memory and `new` and `delete` are keywords rather than functions, so you don't use `(...)` when calling them. 

## new usage
```c++
#include <iostream>

int main() {
	int *iptr = new int;
	*iptr = 10;
	std::cout << "value of iptr " << iptr << std::endl;
	std::cout << "value in *iptr " << *iptr << std::endl;
	return 0;
}
```
`iptr` needs to be freed at some point.


## delete usage
```c++
int *iptr = new int;
*iptr = 1;
delete ptr;
```
After `delete`, the value of `iptr` becomes `0` and address is changed. 

## Dynamic array allocation
No size calculations needed: `T * fresh = new T[n]` allocates an array of `n` elements of type `T`.
- If the type `T` is a built-in type (`int`, `float`, `char`, etc.), then the values are not initialized, like with `malloc`. 
- If `T` is a [`class`](Intro%20to%20OO.md#Overview%20of%20classes), then `T`'s default constructor is called for each element allocated. 

To delete, use `delete[] fresh` to deallocate a pointer returned by `new T[n]`.

- If `T` is not a "built-in" type (`int`, `float`, `char`, etc) then the values are not intiailized, like with `malloc`.
