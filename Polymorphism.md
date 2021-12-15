# Polymorphism
Polymorphism means "many forms". 
```c++
int main() {
	std::vector<Account> my_accounts;
	
	// this is sort of OK (except: "slicing" will occur)
	my_accounts.push_back(CheckingAccount(2000.0));
	
	std::cout << my_accounts.back().type() << std::endl;
	return 0;
}
```
- We have an array of `Account` and we pushed the `CheckingAccount` back into it. It's acceptable to treat this  `CheckingAccount` as an  `Account`  because `CheckingAccount` is a kind of `Account` and has everything that `Account` has because it inherits from it. 
- Each class needs the function `type()` for different outputs.

## Functions
```c++
void print_account_type(const Account& acct) {
	std::cout << acct.type() << std::endl;
}

int main() {
	...
	CheckingAccount checking(1000.0, 2.00);
	...
	print_account_type(checking); // Prints "Account"
	...
}
```
- In main, `checking` has type `CheckingAccount`.
- Passed to `print_account_type()` as `const Account&`
	- This is alloowed because `CheckingAccout` is derived from `Account` and inherits everything from `Account`.

- Prints `Account` because `acct` is treated as an `Account`.  
- Can we force `print_account_type()` to call the function corresponding to the **actual** type (`CheckingAccount`) rather than the locally declared base type (`Account`)?
	- Yes, requires [dynamic binding](Polymorphism#Dynamic%20Binding). 

\
Usually you may use a variable of a derived type **as though it has the base type** because `CheckingAccount` **is-an** `Account`.

## Dynamic Binding
To use it, we declare relevant member functions as `virtual`.
```c++
class Account{
public:
	...
	virtual std::string type() const { return "Account"; } 
};

class CheckingAccount : public Account {
public:
	...
	virtual std::string type() const { return "CheckingAccount"; }
};
```
[`virtual`](Dynamic%20dispatch#Virtual%20Dynamic%20Dispatch) means that the function is essentially virtual and can be replaced by something else. 
- If the derived class implements the same function, then the derived class will override the base class.