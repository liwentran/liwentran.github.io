# Strings
Strings (`std::string`) in C++ are objects, sparing us from details like null terminators. `#include <string>` to use.

Strings can be arbitrarily long. The C++ library handles the memory (allocating and adjusting, freeing when `string` goes out of scope)
## Initializing
```c++
string s1 = "world";
string s2("hello");
string s3(3,'a'); // s3 is "aaa"
string s4; // empty string ""
string s5(s2); // copies s2 into s5

```
s1 is initialized in two steps. s2 is called with constructors.

## Uses
```c++
s = "wow"	// assign literal to string
cin >> s	// put one whitespace-deliminted input word in s
cout << s	// write s to standard out
getline(cin,s)	//read to end of line from stdin, store in s
s1 = s2		//copy contents of s2 into s1
s1 + s2		// return new string: s1 concatenated with s2
s1 += s2	// same as s1.append(s2)
== != <> <= >=	// relational operators; alphabetical order
```

`s.capacity()` returns the bytes of memory allocated
`s.substr(offset, howmany)` gives substring of s
`s.c_str()` returns C-style `const char *` version
`s[5]` accesses the 6th character in string
`s.at(5)` does the same, additionally doing a "bounds check." This is preferred over `s[5]`.

Commonly used [member functions](https://www.cplusplus.com/reference/string/string/):
`s.length()` returns the length of the string (as a long unsigned value)
`empty` returns false when there is at least 1 character
`append` like `+=`
`push_back` like append for a single character
`clear` set to empty string
`insert` insert one string in middle of another
`erase` removes stretch of characters from string
`replace` replace a substring with a given string
