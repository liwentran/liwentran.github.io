# C++ Reference
*Reference variable* is an *alias*, another name for an existing variable (memory location). 
- Used in situations that a pointer would be used in C.
- References have restrictions that make it safer so you don't access invalid memory locations.	
	- References cannot be `NULL` 
	- Must be initialized immediately.
	- Once an alias is set to a variable, it cannot be an alias to another one.
- They provide [pointer](Pointers.md)-like functionality while hiding the raw pointers themselves.

## Declaring References
To declare a reference of type `int`, use `int&`. 

```c++
#include <iostram>
int main() {
	int a = 5;
	int &b = a; // b is another name for a
	int* c = &b; // c is a pointer pointing to a		
}
```

```
&a = 0x7fffd5ef7c44
&b = 0x7fffd5ef7c44
&c = 0x7fffd5ef7c48
c = 0x7fffd5ef7c44
```


## Passing by References
Function parameter with reference type are passed by reference like passing *by pointer* but without the extra syntax inside the function
```c++
// if you have int a = 1, b = 2, then call like this:
// swap (a,b) (no ampersands)!
void swap (int& a, int &b) {
	int tmp = a;
	a = b;
	b = tmp;
}
```
- Looking at the call itself doesn't tel you which parameters are passed by value and which are passed by reference- you have to look at the parameters.

C++ has *both* pass by value (non-reference parameters) and pass by reference (reference parameters).
Functions can have a mix of both pass-by-values and pass-by-references.
 
 When passing objects in C++, we generally pass by reference because no excessive copying occurs, and this decreases runtime. 
 ## Returning References
References can be returned:
 ```c++
 int& minref(int& a, int& b) {
 	if (a<b) {
		return a;
	} else {
		return b
	}
}

int main() {
	int a = 5, b = 10;
	int& min = minref(a,b);
	minref(a, b);
	min = 12;
}
```
- Note: returning a reference to a local variable is as bad as returning a pointer to one. In our original `minref` function, we avoided this by making the parameters themselves references

## Const Reference
A reference can be a `const`. You can't subsequently assign via that reference, but you can still assign the original non-const variable, or via a non-const reference to it.