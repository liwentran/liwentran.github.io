# Intro to Object Oriented Programming

Where as defining new C data types used [`struct`](Structures.md), we use [classes](C++%20Classes) to define new data types in C++. 

## Overview of classes
Features of [classes](C++%20Classes): 
- Include functions that directly operate on the fields.
	- Special functions called *constructors* are used to initialize class objects (also called *instances* - variables declared to be of a class type).
	- Special functions called *destructors* are used to perform clean-up operations just before the lifetime of a class instance ends.
- Add *protection levels* for the fields and functions (e.g. private) to provide data hiding and encapsulation.
- Use *inheritance* to define a class by extending an existing class. 

## stream class Hierarchy
Inheritance: class A inherits from class B if every class A object is-a class B object also. 
![](c++%20stream%20class%20hierarchy.png)
- `istream` and `ostream` are both derived from `ios`.
- `iostream` inherits from both `istream` and `ostream`. 
	- Note that multiple inheritance is allowed. A class can derive from multiple classes 
- steam extraction (`>>`) operator defined for all `istreams` and insertion (`<<`) operator defined for all `ostreams`, and because `fstream` and `stringstream` are both derived from `iostream`, they can use both `<<` and `>>`.

### file input (std::ifstream)
- `ifstream` has a *constructor* taking a string specifying the filename.
	- Calling the constructor with a filename is the same as calling `fopen` with the filename using a `r` flag.
	- The file must already exist.
- since `ifstream` *inherits* from `istream`, we get the insertion (`<<`) operator. 
- `ifstream` has a destructor that closes the file. When the `ifstream` object's lifetime ends, it automatically closes itself.