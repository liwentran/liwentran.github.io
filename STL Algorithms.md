# STL Algorithms
```c++
#include <algorithm>
```
All algorithms can be find on the [reference](http://www.cplusplus.com/reference/algorithm/). 
## Sort
Sort [`vectors`](STL%20Containers.md#Vector) with STL `std:sort` function.

Modifies `vector`, arranging elements in ascending order according to the `<` relation.
- For numbers, `<` means less than
- For strings, `<` means before, in ASCII order.

Specify a region to sort by feeding in an [iterator](STL%20Containers.md#Iterators) to start and end.
```c++
vector<float> grades = {...};
sort(grades.begin(), grades.end()); // sorts everything in grades
```

## Find
Use to search for a particular element in a STL container.
```c++
int arr[] = (1, 20, -2, 4);
int *p;

p = std::find (arr, arr+4, 30); 
```
- First 2 inputs indicates search range
	- The first input is the address to the first element (inclusive)
	- The second input is the address after the last element (exclusive).
- 3rd argument is the search value

If it doesn't find the value, it returns a pointer pointing to one past the last search element. 	

Using `find()` with `vector`:
```c++
vector<int> vec (arr, arr+4);
vecotr<int>::iterator it;
it = std::find(vec.begin(), vec.end(), -2);

if (it!=vec.end())
	cout << "value found at " << *it << '\n';
```

## Count
See how many times a particular vector appears in a STL container.
``` c++
int arr[] = {10, 20, 30, 30, 20, 10, 10, 20}; // 8 elements
int mycount = std::count (arr, arr+8, 10); // 
```

## is_permutation
See if you have the same set of values in two containers: 
```c++
#include <iostrream>	// std::count
#include <algorithm> 	// std::is_permutation
#include <array>	// std::array

int main () {
	std::array<int,5> foo = {1, 2, 3, 4, 5};
	std::array<int,5> bar = {1, 2, 3, 4, 5};
	
	if (std::is_permutation(foo.begin(), foo.end(), bar.begin(0)))
		std::cout << "foo and bar contain the same elements.\n";
	
	return 0; 
}
```
- Takes three inputs: the range of the first STL containers and the first element of the second STL container. No end of second container needed.