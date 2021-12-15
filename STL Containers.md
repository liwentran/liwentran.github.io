# Standard Template Library
STL is C++'s library of useful data structures and algorithms. Similar to `java.util/java.lang` and Python `sets`, `dictionaries`, `collections`.

## STL Containers Overview
- `vector<string>` - vector of `std::strings`
- `vector<float>` - vector of `floats`
- `map<string, int>` - map containing `std::strings` with associated `ints`. Similar to dictionaries. 

Other STL containers:
 - [array](http://www.cplusplus.com/reference/array/array/) – fixed-length array
 - [vector](http://www.cplusplus.com/reference/vector/vector/) – dynamically-sized array
 - [set](http://www.cplusplus.com/reference/set/set/) – set; an element can appear at most once
-  [list](http://www.cplusplus.com/reference/list/list/) – linked list!
- [map](http://www.cplusplus.com/reference/map/map/) – associative list, i.e. dictionary
- [stack](http://www.cplusplus.com/reference/stack/stack/) – last-in first-out (LIFO)
- [deque](http://www.cplusplus.com/reference/deque/deque/) – double-ended queue, flexible combo of LIFO/FIFO
- [unordered_map](http://www.cplusplus.com/reference/unordered_map/unordered_map/) – another map, more like a hash table
- [pair](http://www.cplusplus.com/reference/utility/pair/) – pair template 
- [tuple](http://www.cplusplus.com/reference/tuple/) – like pair, but can have >2 fields

## Templates
Templates are a way of writing an object (`Node`) or function (`print_list`) so that they can work with *any* type. Equivalent of `generics` in Java.

Defining a template is simultaneously defining a *family* of related objects/functions.

### Creating a Template

```c++
template<typename T>
struct Node {
	T payload; // 'T' is a placeholder for a type
	Node *next;
};

template<typename T>
void print_list(Node<T> *head) {
	Node<T> *cur = head;
	while (cur != NULL) {
		cout << cur-> payload << " ";
		cur = cur -> next;
	}
	cout << endl;
}
```
We could replace `T` with `int`, `float`, `char` or `std::string` and this would compile and work. 


```c++
template<typename T>
```
We call the `T` a type variable or type parameter. It can be any name that is a singular capital letter. 

The line makes `Node` a template `struct` and `print_list` a template function.

### Usage
```c++
int main() {
	Node<float> f2 = {95.1f, NULL};
	Node<float> f1 = {35.3f, &f2};
	print_list(&f1);
	
	Node<int> i2 = {230, NULL};
	Node<int> i1 = {34, &i2};
	print_list(&i1);
	
	return 0;
}
```


## Vector
`vector` is an array that automatically grows and shrinks as you need more/less room.
- use `[]` to access elements, like array
- Allocation, resizing, and deallocation handled by C++
- Like `java.util.ArrayList` or Python's `list` type.
- See the [C++ reference](https://www.cplusplus.com/reference/vector/vector/) for more functionality.

To use, `#include <vector>` and `std::vector<char>`

### Usage
```c++
// declaration
using std:: vector;
vector<std::string> names;
 
// add elements to vector (at the back) 
names.push_back("Alex");
names.push_back("Ben");

// print the number of items, and first and last items:
cout << "Size = " << names.size()
	 << ", first =" << names.front()
	 << ", last =" << names.back() << endl;
```

Print all elements of a vector with indexing:
```c++
for (size_t i = 0; i < names.size(); i++) {
	cout <<names[i] << endl;
}
```

### Iterate through a Vector
With an [*iterator*](STL%20Containers.md#Iterators):
```c++ 
for (vector<string>::iterator it = names.begin();
	it != names.end();
	++it) {
	cout << *it << endl;
}
```
- Iterators are separate types. They are "clever pointers" that know how to move over the components of a data structure (like a vector, linked list, or tree). They are safer and less error-prone than pointers.

For STL container of type `T`, iterator has type `T::iterator`:
```c++ 
for (vector<string>::iterator it = names.begin(); it != names.end(); ++it) {
	cout << *it <<endl;
}
cout << endl;
```
 - `.begin()` give access to the first element.
 - `.end()` is one past the last element.

Iterate in *reverse* order by using `T::reverse_iterator`, `.rbegin()` and `.rend()`:
```c++
for (vector<string>::reverse_iteartor it = names.rbegin(); it != names.rend(); ++it) {
	cout << *it <<endl;
}
```
- `.rend()` gives access to the last element
- `.rbegin()` give access to one before the first element
- `++` on a reverse iterator goes backwards (overloaded).



## Map

Declaration:
```c++
map<int, string> id_to_name;
```

Add a key `+` value to a map. A map can only associate 1 value with a key:
```c++
id_to_name[342] = "Alex";
id_to_name[342] = "George"; // "Alex" is replaced
```

Print a key and associated value:
```c++
const int k = 342
cout << "Key=" << k << ", Value=" << id_to_name[k] <<endl
```

Get the number of keys:
```c++
id_to_name.size()
```

Check if map contains (has a value for) a given key using `.find()`, which returns an iterator to the location where it was found. Dereferencing that iterator will give you that pair of key and value.
```c++
if (id_to_name.find(342) != id_to_name(end))
  cout << "Found it" << endl;
 else 
   cout << "Not found" << endl; 
```

## Iterate through map
Visit all the elements of the map using an [*iterator*](STL%20Containers.md#Iterators) of type `map<int,string>::iterator>`. The loop is similar to the [loop for vector](STL%20Containers.md#Iterate%20through%20a%20Vector). Iterator will move over the keys in *ascending order*. 
```c++
for (map<int,string>::iterator it = id_to_name.begin(); it != id_to_name.end(); ++it)
  cout << " " << it->first << ": " << it->second << endl;
```
- it->first is the key 
- it->second is the value
- Use `reverse_iterator`, `.rbegin()`, `.rend()` to get keys in *descending* order.
 

 ## Pairs
 
 How can we implement a function that returns multiple values? For example, `divmod(10,5)` should return `2` (quotient), `0` (remainder). 
 
 1. Pass-by-pointer arguments: 
```c++
void divmod(int a, int b, int *quo, int *rem) {
	*quo = a/b;
	*rem = a%b;
}
```
2. Define a `struct` 
```c++
struct quo_rem {
	int quotient;
	int remainder;
};

struct quo_rem divmod(int a, int b) {...}
```
 3. Use a `pair` to return multiple values
```c++
#include <utility> // where pair and make_pair are defined
using std::pair; using std::make_pair;

pair<int, int> divmod(int a, int b) {
 	return make_pair(a/b, a%b)
}
```

## Usage of Pair in Maps
A dereferenced [`map` iterator](STL%20Containers.md#Iterate%20through%20map) is a key, value pair. 

## Properties of pair
Relational operators for `pair` work as expected:
- Compares first field first
- If there's a tie, compares second field.

`make_pair(2,3) < make_pair(3,2)` is true

More about pair on its [reference page](www.cplusplus.com/reference/utility/pair/).

## typedef
Iterator types can be complex (e.g. `map<string, map<string, int>>` is an iterator over a `map` where the value is a `map`).


Use `typedef` to give shorter names to types to reduce clutter and bring related type declarations closer together 
```c++
typedef map<int, string> Tmap; // map type
typedef TMap::iterator TMapItr; // map iterator type
```

# Tuple
`tuple` is like `pair` but with as many fields as you like
```c++
#include <tuple>
using std::tuple; using std::make_tuple;

tuple<int, int, float> divmod(int a, int b) {
	return make_tuple(a/b, a%b, (float)a/b);
}
```

`get<N>(tup)` gets the `N`th (starts at `0`) field of variable `tup`.

## Iterators
There are four types of iterators:

| type | `++it` | `--it` | Get with | `*it` type |
|---|---|---|---|---|
|`iterator`|forward|back|`.begin()`/`end()` |-|
|`const_iterator`|forward|back|`.cbegin()`/`cend()`|`const`|
|`reverse_iterator`|back|forward|`.rbegin()`/`rend()` |-|
|`const_reverse_iterator`|back|forward|`.crbegin()`/`crend()`|`const`|

Example usage in [vector](STL%20Containers.md#Iterate%20through%20a%20Vector) and [map](STL%20Containers.md#Iterate%20through%20map).

 ### Const Iterators
 `const_iterator` *does not* allow modifications to the values the iterator is pointing to. All values are `const` protected. 
 
 Attempts to change will return an error saying `assignment of read-only`. 
