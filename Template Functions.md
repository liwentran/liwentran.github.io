# Template Function
Template allow us to write functions or class once but get a whole family of overload specifications:
```c++
template< typename T >
void fun(const T& input) { ... }

void fun(const int& input) { ... }
void fun(const float& input) { ... }
void fun(const char& input) { ... }
void fun(const MyClass& input) { ... }
```

Recall: two functions are [overloaded](Overloading.md#Function%20Overloading) if they have the same name and return type, but have different parameter types. 

## When to use?
When you find yourself writing functions with essentially the same body, but for different types.
Repetitive code is a sign of bad design because if a correction or modification for one of the functions also has to made for any other we've made. 

## Example 
```c++
template< typename T>
int sum_every_other(const T& ls) {
	int total = 0;
	for (typename T::const_iterator it = ls.cbegin(); it != ls.cend(); ++it) {
		total += *it;
		if (++it == ls.cend()) break;
	}
}
```
- If we pass `std::vector<int>`appropriately function overload. 
- When we need to use a nested class (like in this format: `::const_iterator`) in the template, then you need to tell the compiler that it really is the type by using type name here.