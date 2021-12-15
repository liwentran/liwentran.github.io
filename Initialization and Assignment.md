# Initialization and Assignment

## Difference between `=` and `==`
There are two types of `=`:
- `=` in a declaration, like `int a = 4;`(initialization).
- `=` elsewhere, like `a = 4;` (assignment).

##  Example
```c++
//complex.h 
#ifndef COMPLEX_H__
#define COMPLEX_H__
#include <iostream>

class Complex {
public:
	// Default constructor
	Complex(): Complex(0.0, 0.0) { std::cout << "Default" << std::endl }
	// Non-default constructor
	Complex(double r, double i): real(r), imag(i) { std::cout << "Non-default" << std::endl; }
	// Copy constructor
	Complex(const Complex& oeprator=(const Complex& rhs)  {
		std::cout << "Assign" << std::endl;
		real = rhs.real;
		imag = rhs.imag;
		return *this;
	}
	
	double get_real() const { return real; }
	double get_imag() const { return imag; }
private:
	double real, imag;
};
#edif // COMPLEX_H__
	
```

```c++
// complex_main.cpp
#include "complex.h"

int main() {
 Complex c; 				// default (no-argument) constructor call
 Complex c2 = {4.09, 0.5}	// = in declaration: *initialization*
 Complex c3 = c; 			// = in declaration: also *initialization*
 c3 = c2; 					// = outside declaration: *assignmment*
 if (c3.get_real() == 4.9) {// == is *equality testing*
 std::cout << "Real part of c3 is equal to 4.9" << std::endl;

 }

 return 0

}
```
```shell
//output
Non-default
Default
Non-Default
Copy
Assign
```
- The first two outputs come from `Complex c;` because the default constructor calls on the non-default constructor. 