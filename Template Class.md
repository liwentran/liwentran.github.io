# Template Class
## Example
```c++
//template_class.h
#include <iostream>

template< typename T>
class Node {
public: 
	Node(T pay, Node<T> *nx) : payload(pay), next(nx) { }
	
	void print() const {
		const Node<T> *cur = this;
		while(cur != NULL) {
			std::cout << cur->payload << ' ';
			cur = cur ->next;
		}
		std::cout << std::endl;
	}
	
private:
	T payload;
	Node<T> *next;
};
```
# Template classes and header files
If we separate this template class into a `.h` file and `.cpp` file we get ERRORS:
```c++
//template_class2.h
#ifndef NODE_TEMPLATE_H__
#define NODE_TEMPLATE_H__
template< typename T >
public:
class Node {
	Node(T pay, Node<T> *nx) : payload(pay), next(nx) {}
	void print() const;
private:
	T payload;
	Node<T> *nx;
};
```
```c++
//template_class2.cpp
#include "template_class2.h"
#include <iostream>

template< typename T> 
void Node<T>::print() const {
 	const Node<T> *cur = this;
	while(cur != NULL) {
		std::cout << cur ->payload << ' ';
		cur = cur->next;
	}
	std::cout << std::endl;
}
```
When we try to use it we get errors in certain areas:
```c++
Node<float> f3 = {95.1f, NULL}; // instantiates Node<float>
Node<float> f2 = {34.4f, f3};
d2.print(); // instantiate Node<float>::print

Node<int> i2 = {32, NULL}; // instantiates Node<int>
Node<int> i1 = {3, i2};
i1.print(); // instantiates Node<int>::print
```
- When instantiating, compiler needs the relevant template classes and functions to be fully defined already because the compiler acts **lazily** when initiating templates. 
	- Lazily instantiating `Node<float>` and `Node<int>` is fine because both are defined in the header.
	- Instantiating `Node<float>::print()` and `Node<int>::print()` won't work because they are in separate source file that is not `#include`d (by convention we never `#include#` `cpp` files)
- In contrast to typical functions or class use, where definition can be in separate `.cpp` files. i.e. template classes have to be typically defined in the header files. 
- Solutions:
	- Move `Node<T>::print()` definition back into header.
	- Put member function definitions in a separate file and include it, but don't give it a `cpp` extension. i.e. a different extension such as `inc` or `.inl` and use `#inlcude "template_class2.inc"` along with `#inlcude "template_class2.h"` (or use `#inlcude "template_class2.inc"` at the end of the header file).