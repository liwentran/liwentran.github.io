# I/O Streams
## I/O
Overview of `iostream`, the main C++ Library for input and output:
```c++
#include <iostream>

using std::cin; // default input stream
using std::cout; // default output stream
using std::endl; // end of line, flushes buffer
using std::cerr; //default error output stream
```

### cout

```c++
cout << "Hello world!" << endl;
```
- `cout` prints to the standard output stream (like `stdout` in C).
- `endl` is the new line character. 
- `<<` is the *insert output* which allows you to insert something into a stream.  

There are no format specifier (`%d`, `%s`, etc.). Items that need to be printed are arranged in printing order, which is easier to read and understand. However, if you still want to use it, it does work after including `<cstdio>`. 

### cin
```c++
string name;
cin >> name;
```
- `>>` is the extract operator. Collects from standard input and stores it into the variable provided. 
- `cin` is mapped to standard input. It reads one whitespace-delimited token from standard input and places the result in the string `name`. 
- Note: both are part of standard namespace: `using std::cin` and `using std::string`

 If you input an entire sentence, it will still read one token at a time (word by word per iteration). This code will store the smallest word in an inputted sentence and print it out. 
 ```c++
 string word, smallest; 
 while (cin >> word) {
 	if(smallest.empty() || word < smallest) {
		samllest = word;
	}
 }
 count << smallest < endl; 
 ```
 - Note: relational operators work with strings. (operators were overloaded). 

```c++
cin.get(ch)
```
- Reads one character from the standard input

### Chaining
In the [above example](IO%20Streams.md#cout), we send two things to `cout`, this is called *chaining*. The insert operator joins all the items to write in a "chain". 
The leftmost item in the chain is the stream being written to. 
```c++
cout << "We have " << inventory << " " << item << "s left." << endl;
```
`inventory` and `item` are variables. 

### Operator Overloading
`<<` usually does bitwise left-shift; but if operand on the left is a C++ stream (`cout`), `<<` is the insert operator. Shifting only applies to numbers. 
More on this later. 

## File I/O
In C we used `fprintf` and `fscanf` to read and write from files. In C++,  `std::ofstream` and `std::instream` are their counterparts. 
These are defined in the file-stream header: `#include <fstream>` and still use the `<<` and `>>` operators. 
- `ofstream` for writing to a file
- `ifstream` for reading from a file
- `fstream` for reading and writing to/from a file.

### Examples
ofstream:
```c++
#include <iostream>
#include <fstream>
int main() {
	std::ofstream ofile("hello.txt");
	ofile << "Hello world!" << std::endl;
	return 0;
}
```
This program writes "`Hello world!`" to a text file named "`hello.txt`".


ifstream:
```c++
#include <iostream>
#include <fstream>
#inclue <string>
int main() {
	std::ifstream ifile("hello.txt");
	std::string word; 
	while( ifile >> word )
		std::cout << word <<std::endl;
	return 0;
}
```
This program will print
```shell
Hello,
World!
```

## I/O from/to strings
```c++
std::stringstream
```
Instead of reading or writing to console or file, it reads and writes to a temporary string ("buffer") stored inside. Useful for programs that process strings, like one that parses input. 
```c++
#include <iostream>
#include <sstream>

int main() {
	std:stringstream ss; // create object
	ss << "Hello, world!"" << std::endl;
	std::cout << ss.str();
	return 0;
}
```

### stringstream details
- A string buffer that contains a sequence of characters.
- Call `str()` function on a `stringstream` to create a string from that `stringstream` to get the content of the buffer.
- `str(string)` sets the content of the buffer to the string argument.
	- For example, `std::stringstream ss("Ali")` creates a `stringstream` buffer and puts `"Ali"` into that stream. 
- `<<` and `>>` operators can be used with `stringstream` to insert/extract content.

`stringstream` also comes in flavors that only do reading or writing:
- `istringstream` <-> `ifstream`
- `ostringstream` <-> `ostream`

### example
```c++
int num;
std::string word1, word2;

ss << "Hello" << ' ' << 2019 << " world";
ss >> word1 >> num >> word2;
```
This will store `Hello` into `word1`, `2019` into `num`, and `world` into `word2`.