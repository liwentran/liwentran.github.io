# Exceptions
We use exceptions to indicate that a **fatal error** has occurred, where there is no reasonable way to continue from the point of error, but it might be possible to continue from **somewhere else**, but not from the point of error
```c++
// exceptions1.cpp
#include <iostream>

int main() {
	size_t mem = 1;
	while (true) {
		char *lots_of_mem = new char[mem];
		delete[] lots_of_mem;
		mem*=2;
	}
	std::cout << "Forever is a long time" << std::endl;
	return 0;
}
```
- Output:
```c++
$ ./exceptions1
terminate called after throwing an instance of 'std::bad_alloc'
	what(): std::bad_alloc
Aborted (core dumped)
```
- This program keeps allocating bigger arrays until an allocation fails. 
- The exception has been trown here because any pointer returned by `new[]` wouldn't be usable; program doesn't necessarily expect that. 
	- Program can signal that it **does** expect that by **catching** the appropriate exception. (If it doesn't do that, the exception crashes the program)

## Exception Class
Standard exceptions:
<img src="https://www.cs.uah.edu/~rcoleman/CS307/SelectedTopics/Images/ExceptionClasses.jpg"
	 width="70%"/> 

If you want to implement your own exception, you can inherit one of them.

## Example exception mechanism
Use the `try` `catch` keywords
```c++
// exceptions2.cpp
#include <iostream>
#include <new> //bad_alloc defined here
int main() {
	size_t mem = 1;
	char *lots_of_mem;
	try {
		while(true) {
			lots_of_mem = new char[mem];
			delete[] lots_of_mem;
			mem*=2;
		}
	}
	catch (const std::bad_alloc& ex) {
		std::cout << "got a bad_alloc"
			<< std:: endl << ex.what() << std::endl;
	}
	std::cout << "Forever is a long time" << std::endl;
	return 0;
}
```
```
$ ./exceptions2
got a bad alloc
std::badd_alloc
Forever is a long time
```

\
Always guaranteeing that you catch out of range exceptions:
```c++
// exceptions3.cpp
#include <iostream>
#include <vector>
#include <stdexcept> // standard exception classes defined

int main() {
	std::vector<int> vec = {1, 2, 3};
	try {
		std::cout << vec.at(3) << std::endl;
	} catch (const std::out_of_range& e) {
		std::cout << "Exception: " << std::endl << e.what() << std::endl;
	} 
	return 0;
}
```
```
$ ./exceptions3
Exception:
vector::_M_range_check __n (which is 3) >= this->size() (which is 3)
```

### Exceptions thrown by `new`
```c++
char *lots_of_mem = new char[mem];
```
Why doesn't `new[]` return `NULL` on failure, like `malloc`?
- When the call stack is deep: `f1() -> f2() -> ...` propagating errors backwards requires much coordination. 
- If any functions fails to propagate error back, the chain is broken.
- Error encoding must be managed (e.g. 1= success, 2 = out of memory, ...); no standard (`enum` helps but is not perfect). 

Exceptions are more flexible; often less error prone, more concise than manually propagating errors back through the chain of callers. 

\
Looking in the [documentation](https://www.cplusplus.com/reference/new/operator%20new/) for `new`/`new T[n]`, you can see the exception thrown is of type `bad_alloc`. 

## Keywords
Keyword `try` marks block of code where an exception might be thrown. It tells C++: "exceptions might be thrown, and I'm read to handle some or all of them".
```c++
try {
	while(true) {
		lots_of_mem = new char[mem];
		delete[] lots_of_mem;
		mem*=2;
	}
}
```

\
The `catch` block, immediately after the `try` block, says what to do in the event of a particular exception.
```c++
	catch(const bad_alloc& ex) {
		std::cout << "yelo, got a bad_alloc" << std::endl;
	}
```
- If you catch a base exception class, you can handle a family of exceptions that inherits from this base exception class. (e.g. catch `std::exception` to handle all exceptions, catch `std::runtime_error` to handle `std::range_error`, `std::overflow_error`, `std::underflow_error`)

\
There can be multiple `catch` blocks for one `try` statement.
- The specific catch statements should come before the most general exceptions. 
- C++ will pass control to the **first** `catch` block whose type equals or is the base class of the thrown exception. 
## Unwinding
The point in the program where the exception is actually thrown is called the **throw point**. 
When exception is thrown, we **don't** proceed to the next statement, instead we follow a process of "unwinding"

\
Unwinding: keep moving "up" to wider enclosing scopes; stop at `try` block with relevant `catch` clause.
If we unwind all the way to the point where our scope is an entire function, we jump back to the caller and continue unwinding. 
If exception is never caught - i.e. we unwind all the way through `main` - exception info is printed to console and program exits. 

\
For example, when `runtime_error` is thrown, it will keep moving up to wider enclosing scopes, stop at `try` block and continue with the relevant `catch` block. 
```
if (a==b) {
	try {
		while {
			try {
				if(d%3 == 1) {
				throw std::runtime_error("!");
			}
			catch (const bad_alloc &e) {
				...
			}
		}
	}
	catch (const runtime_error &e) {
		// after throw, control moves here
	}
}
```
It will even jump back to the caller and continue unwinding. 

\
Unwinding will cause local variables to go out of scope, so destructors will always be called, regardless of whether scope is exited because of reaching end, `return`, `break`, `continue`, `exception`, ... 

# Customizing Exceptions
You can define your own exception class, derived from `std::exception`. 
Since `exceptions` are related through inheritance, you can choose whether to catch a base class (thereby catching more different things) or a derived class.

## Example custommized exception
Exception for a game-card program:
```c++
class BadCardError : public std::runtime_error {
public:
	BadCardError (Card c) :
	std::runtime_error("bad card"), card(c) { }
private:
	Card card;
};
```

