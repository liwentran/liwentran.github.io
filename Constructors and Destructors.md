# Constructors

A constructor is a member function you can define yourself that initializes [`class`](C++%20Classes.md) and decides how fields should be initialized. There are a few rules:

- Define the constructor as `public`
- The function name must match the class name exactly. 
- If it takes no arguments, it is called  a **default** constructor. 	

- Provide at least one constructor or the compiler generates a default one for you.
- See a good example of all the different [examples here](Initialization%20and%20Assignment.md#Example).

## Default Constructors

The **default** constructor for a class is a member function that C++ calls when you declare a new variable of that class without any initialization, or when a constructor takes no arguments.

```c++
class Rectangle {
public:
    //default constructor for Rectangle
    Rectangle() { ... }
    ...
}
```



What does a compiler-generated default constructor do? For each member field:

- If it is a built-in type (`int`, `doubles`, ...) it isn’t initialized (so it has a garbage value).
- If it is a class type, the default constructor for that class type is called. 


A constructor is called implicitly when a new object is declared or explicitly when one is created using `new`.

If we created our own constructor, the compiler won’t generate any constructor for us.


## Constructor Initializer List

Define our own default constructor to initialize values:

```c++
class Rectangle {
public:
    Rectange(): width(0.0), height(0.0) { }
private:
    double width, height; 
}
```

If the dimensions were objects themselves, we could call the object’s constructor here (e.g. `list()` where `list` is a `vector<int`>).



Which is the better method? 

```c++
// initializer list style
IntAndString(): i(7), s("hello") { }

// other method
IntAndString() {
    i = 7;
    s = "hello";
}
```

The initializer list is the better choice because it works as expected, even for reference variables. Furthermore, we can use default or non-default constructors to initialize fields: `IntAndString(): i(7), s(“hello”) { }`. This reduces the extra step that `s = “hello”` does of first being initialized and then set, wastefully. 

## Non-Default Constructors
Constructors can take arguments, allowing the caller to "customize" the object.
Example using initializer list:
```c++
class DefaultSeven {
public:
	DefaultSeven(int initial): i(initial) { } 
	
	int get_i() {return i;}

private:
	int i;
};
```

When we supply an alternative (non-default) constructor, there is no implicitly-created default constructor by the compiler. 

### Default Arguments
- In C++ we can specify default values for function arguments in the definition.
- We can then omit parameters when calling the function, but only sequentially from right to left. 
- Default argument values create several functions in one. 
- This applies to functions in classes, as well as any other function.
- Useful when creating multiple constructors.
	- If include default values for all arguments, this results in usage as a default (parameter-less) constructor.

Example of constructor with default arguments.
```c++
class DefaultSeven {
public:
	// three ways to call constructor 
	DefaultSeven(int initial = 7, double val = .5): i(initial), v(val) { } 
	
	int get_i() {return i;}
	double get_v() {return v;}
private:
	int i;
	double v;
};

int main() {
	DefaultSeven one(10,20), two(2), tre
}
```

What happens when a constructor parameter has the same name as the instance variable it is supposed to initialize (`MyClass(int init) : init(init) { }`)? It would be okay in an initializer list because context makes it okay.



# Destructor
`new` as mentioned in [C++ Dynamic Allocation](C++%20Dynamic%20Allocation.md) will call the default constructor of our class.

A class `constructor`'s job is to initialize the fields of the object, it is also common for a constructor to obtain a resource (allocate memory, open a file, etc.) that should be released when the object is destroyed (deallocate memory, close a file, etc.).

A class `destructor` is a method called by C++ when the object's lifetime ends or it is otherwise deallocated (ie, with `delete`). It is always automatically called when object's lifetime ends, including when it is deallocated. However, the destructor of an object is not necessarily called if there are no references or pointers to an object because there is no tracking. 

A destructor's name is the class name prepended with `~`, e.g. `~Rectangle()`.

Example:
```c++
#ifndef SEQUENCE_H
#define SEQUENCE_H
#include <cassert>
class Sequence {
public:
	Sequence() : array(NULL), size(0) { }
	Sequence(int sz) : array (new int[sz], size(sz) {
		for (int i = 0; i < sz; i++) array[i] = i;
	}
	~Sequence() { delete[] array; }
	int at(int i) {
		assert(i<size);
		return array[i];
	}
private:
	int *array;
	int size;
};
#end if // SEQUENCE_H
```

Destructors are always a better option than creating a special member function for releasing resources like `void clean_up() { delete[] array; }` because sometimes main will return before reaching `clean_up()`.