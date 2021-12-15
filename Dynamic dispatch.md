# Dynamic Dispatch
## Memory Layout
For this simple class:
```c++
class Account {
public: 
	Account() : balance(0.0) { }
	Account(double initial) : balance(initial) { }
	
	void credit (double amt) {
		balance += amt;
	}
	
	void debit (double amt) {
		balance -= amt;
	}
	
	double get_balance() const {
		return balance;
	}
	std::string type() const {
		return "Acccount";
	}
private:
	double balance;
}
```
Stack segment:
- double Account::balance

Code segment:
- Account::Account()
- Account::Account(double)
- Account::credit(double)
- Account::debit(double)
- double Account::get_balance()
- std::string Account::get_type()

\
The memory layout of a derived class would have all of the above plus more at the end. 
## Object Slicing
When a compiler lays out a derived object in memory, it pus the data of the base class first. 
We can convert from a derived class back to its base class. 
- The compiler **slices out** the derived class, i.e. ignores the contents of [memory](Dynamic%20dispatch#Memory%20Layout) past the base data. 
## Virtual (Dynamic Dispatch)
Use the `virtual` keyword to indicate a method to be overridden by the derived class. 

\
The [memory layout](Dynamic%20dispatch#Memory%20Layout) of the `Account` class with `virtual` function `type()` would look like this:

Stack segment:
- double Account::balance
- Account::\_vptr -> a virtual table
	- type_info Account
	- Address of std::string Account::type()

Code segment:
- Account::Account()
- Account::Account(double)
- Account::credit(double)
- Account::debit(double)
- double Account::get_balance()
- std::string Account::get_type()

\
When you look at the derived class, the pointer would look like:
- Account::\_vptr -> a virtual table
	- type_info CheckingAccount
	- Address of std::string CheckingAccount::type()

## Override
It's a typical mistake to believe you had override a function when you have not. Often because:
- Fail to match `const` status
- Fail to exactly match parameters and return types

\
The keyword `override` helps. When you intend to override a function, add the `override` modifier:
```c
class Account {
public:
	virtual std::string tpe() const { return "Account"; } 
};

class CheckingAccount : public Account {
public:
	std::string type() const override { return "CheckingAccount"; }
};
```

This way, if you failed to match the functions, it will throw a warning. 

## Pass by-value vs by-reference
When you pass by-value, a [copy constructor](Overloading.md#Copy%20constructor) is called to create a copy of the passing object. It takes in the passing object as a reference (object slicing happens in the constructor), but the new created object is using the base class memory layout, which means the virtual function is pointing to `Account::type()`. 

So, a function that takes in pass-by values will not be able to take advantage of overriding. 