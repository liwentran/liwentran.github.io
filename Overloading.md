Overloading means piling on another definition for a name. 

# Function Overloading
C++ compiler can distinguish functions with the same name but different parameters
```c++
// overloading1.cpp
void output_type(int) { std::cout << "in" << std::endl;}
void output_type(float) { std::cout << "float" << std::endl;}

int main() {
	output_type(1); // will print int
	output_type(1.f); // will print float
	return 0
}
```

However, it cannot distinguish functions with the same name and parameters but different return types. 

# Operator Overloading
Operators like `+`  and `<<` are like functions:
- `a + b` is like `plus(a, b)` or `a.plus(b)`
- `a + b + c` is like `plus(plus(a,b),c) `
- If it is like a function, then it can be overloaded.

C++ allows us to define new classes, and we can define new meanings for operators (`+-*/¡—&=[]==!=<<`, etc.)so we can use them on these type. 

Operator overloading differs from function overriding, where we replace a definition of a name 

To specify a new definition for an operator with symbol S, we define a method called `operatorS`. 
The compiler understands that expressions using the infix operator `+` applied to the types specified in the method should map to the above function. 

## Example: Output Operator
If we had a variable `const std::vector<int> vec = {1,2,3};` can make `std::cout << vec <<std::endl` work by defining the appropriate function.
```c++
std::ostream& operator<<(std::ostream& os, const std::vector<int>& vec) {
	for (std::vector<int>::const_iterator it = vec.cbegin();
	it!=vec.cend(); ++it) {
		os<<*it<<' ';
	}
	return os;
}
```
- `std::ostream` is a C++ output stream. We can write to it; cannot read from it. 
- It is `std::cout's` type (can be passed as parameter of type).
	- `const std::ostream&` won't work because it disallows writing. 

- Taking as first parameter and returning `std::ostream& os` enables chaining. 
- Taking `const vector<int>&` as  the second parameter allows `std::vector<int>` to appear as a right operand in a `operator<<` call. 

To output a value, we may need access to instance variables, which are `private`. However, we can't make `operator<<` a member of the `Rational` class (described in the next section) since a member function would get the object of that class type as its implicit argument, and the first argument for `<<` needs to be `std::ostream` type (not `Rational`). 
- Still, we can use the `friend` keyword to give the member "almost-member" status. It says that the method is trusted by the class, meaning it is allowed access to private member variables, but not an actual member of the class:
- Why do we need `friend`? When the argument is not of your class type (`ostream`), then it cannot be a member of your class type. 
 ```c++
class Rational{
public:
	...
	friend ostream& operator<<(ostream& os, const Rational &r);
	...
private:
}
```

## Assignment Operator
`operator=` is called when assigning one `class` variable to another except for initialization; [copy constructor](Overloading.md#Copy%20constructor) handles that.

Example:
```c++
Image& operator=(const Image& o) {
	delete[] image; // deallocate previous image memory
	nrow = o.nrow;
	ncol = o.ncol;
	image = new char[nrow*ncol];
	for (int i = 0; i < nrow * ncol; i++) {
		image[i] = o.image[i];
	)
	return *this; // for chaining
}
```

## Operator as Instance Method
Suppose we have a defined class `Rational` that stores an `int numerator` and `int denominator`, the best way to declare a method named `operator+` to work two `Rational` objects would be as a member of the `Rational` class since the method needs to access the `private` instance variables:
```c++
Rational operator+ (const Rational& right) const;
```
- Only one explicit argument and one implicit argument (the item pointed to by `this`). 
- The last `const` in that line promises not to modify the implicit object. 

Full class:
```c++
// operator4.h
class Rational {
public: 
	Rational operator+(const Rational& right) const;
	
private:
	int num;
	int den;
};

// operator4.cpp
Rational Rational::operator+(const Rational& right) const {
	int sum_num =
	this->num * right.den + right.num * this->den;
	int sum_den = this->den * right.den;
	Rational result(sum_num, sum_den);
	return result;
}
```
- Notice that the return type is not a reference nor a pointer. When the `operator+` method returns its locally-declared result object, the [**copy constructor**](Overloading.md#Copy%20constructor) of the class is called to make a copy of `result` before the stack frame is popped.
	`Rational(const Rational& original);`
	
# Copy constructor
If you don't define a copy constructor, a default one is created for you (implicit; compiler-generated) which performs a **shallow copy** (simple field-by-field copy). This would not work if your class manages heap memory. 
- If one of your member fields is a pointer, the default copy constructor would simply copy the address (and not the heap memory). The copy's pointer would point to the same address. This would be problematic because free would be run twice on that memory address. The class fields will have have their corresponding copy constructor or assignment operator functions called. 
- Instead, we want a **deep copy** (new buffer created and contents coped).

Copy constructor is used:
- When making an explicit call to a constructor feeding it an already-created class object.
	`Image o_wins = x_wins;` has the same meaning as `Image o_win(x_wins);`
- When sending a class object to a function using pass-by-value.
- When a class object is returned from a function by value.

Copy constructor initializes a `class` variable as a copy of another. 
```c++
ClassName(const ClassName&)
```