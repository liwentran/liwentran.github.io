# C++ Classes
We already know about [`structs`](Structures.md) which bring together several variables that describe a "thing." However, to implement functions, we'd have to pass the `struct` by value. 

In the object oriented way, we prefer to have related functionality (`print_rectangle`, `area` for a rectangle class) be part of the object (the `struct`)

## What is a class
- A class definition is like a *blueprint* defining a type.
- Objects of that type are created from that *blueprint*
- Once we define a class, we have one blueprint from which we can create 0 or more objects.
- Each of the objects is an *instance* of the class and has its own copies of all instance variables.

## Writing C++ Classes
- Class definition goes in a `.h` file. 
 - Functions can be declared and defined inside `class {...}`.
 - Only define member functions inside the class definition if it's *very* short. This is called "in-lining" the function definition. Otherwise, put a prototype in the class definition and define the member function in a `.cpp` file.
	 - You'll need to qualify the function with the class scope such as `Classname::function(){}` in the `.cpp` file.
	 - Do not try to initial class fields immediately when they are declared. E.g., `double width = 10;`  because this is allowed for static fields.

### const modifier
```c++
void print() const {
	...
}
```
- The use of `const` as modifier in method header indicates that the function will not modify any member fields.
- `const` can be used for member fields too.

### Examples
In-lining example:
```c++
// rectangle.h
#ifndef RECTANGLE_H
#define RECTANGE_H

class Rectangle {
	...
	double area() const {
	// in-lining
	return width*height;
	}
	...
};
#endif //RECTANGLE_H
```

 Defining a function outside class:
 ```c++
 // rectangle.h
 #ifndef RECTANGLE_H
 #define RECTANGLE_H
 
 class Rectangle {
 	...
	double area() const;
	...
}
#endif //RECTANGLE_H
 ```
```c++
// rectangle.cpp
#include "rectangle.h"

double Rectangle::area() const {
	//define outside class
	return width * height;
}
```

class2.cpp:
```c++
#include <iostream>

class Rectangle {
public:
	double width;
	double height;
	
	void print() const {
		std::cout << "width=" << width << ", height=" << height << std::endl;
	}
	
	double area() const {
		return width*height;
	}
};

int main() {
	Rectangle r = {30.0, 40.0};
	r.print();
	std::cout << "area=" << r.area() << std;;endl;
	return 0;
}
```
- Notice that the member functions doesn't need to pass in the parameters since they can directly access the fields because they are in the same class. 

## Protection
Fields and member functions can be `public`, `private`, or `protected`. 
- A `public` field or member function can be accessed freely by any code with access to the class definition (code that includes the `.h` file).
- A `private` field or member function can be accessed from other member functions in the class, but **not** by a user of the class.
	- Base-class members marked `private` cannot be accessed from member functions defined in the derived class. (They are still there, only derived class member functions can't use them without `public` or `protected` accessor or mutator functions)
We use `public:` and `private:` to divide class definition into sections according to whether members are `public` or `private`.
`private` is default.

How to section:
```c++
class Rectangle {
public:
	...
	double area() const {
	//definition inside class
	return width * height;
	}
	...
private:
	double width, height;
};
```
\
- A `protected` field or member functions can be accessed from member functions of their class and from functions defined in derived classes.
	- Based class members marked `public` or `protected` can be accessed from member functions defined in the derived class


## `this` pointer
When another member function has a parameter with the same name as the instance variable it is supposed to initialize, the local variable (parameter) will hide the instance variable.
`this` is a *pointer* to the instance variable and can be used to clarify.
- `this->init` always refers to the instance variable `init`.

We don't use `this` unless necessary in C++, unlike Java, where it is a good style to always qualify instance members.

## Array of Objects
Declaring an array of a class type makes *all* the objects, calling the [default constructor](Constructors%20and%20Destructors.md#Default%20Constructors) to create each one. Thus, requires the class to have a default constructor.

What if you don't want to have default constructor?
1. List 
Use list-initialization to initialize each object in the array.
`MyThing s[3] = {{3}, {2}, {4}};`
Every value inside will be the engines for the objects. `MyThing` only has one member field, so we only provide one value. This is called listing test when we initialize structures by passing in different values. 

2. use `STL` to reserve some element size
```c++
int main() {
	// empty vector and reserve 10 element size
	std::vector<MyThing> s;
	s.reserve(10);
	
	// initialization using emplace_back
	for (int i = 0; i < 10; ++i) s.emplace_back(i);
}
```

