# Inheritance

## Relationships
Inheritance models an **is-a** relationship. 
	- E.g., a checking account *is a* kind of account.
	\
Composition or aggregation models a **has-a** relationship.
	- E.g., a grade list that *has a* vector of grades as part of it. 

## Inheritance Hierarchy
We can have multi level inheritance and have a derived class that inherits from multiple base class. 

## Declaration and Terminology
```c++
class BaseClass {
	// definitions
};
class DerivedClass: public BaseClass {
	// definitions
}
```
- **Derived class** inherits from **base class**. 
	- In Java-like vocab: "subclass inherits from superclass".

- This is a **public inheritance** (most common)
	- Access of members in the base class is passed down and preserved.
- `protected` & `private` inheritance is possible (not common). If you forget to explicitly say `public`, the default is `private`
	- `protected` inheritance means you will inherit all the `public` and `protected` members as `protected` field. That means all the `public` member fields/functions in the base class, after your inheritance in the derived class, will become `protected` member fields/functions. This means that future classes that derive from this derived class will not be able to access it. 
	- `private` inheritance is even stronger. All `public` or `protected` fields/functions will become `private` in the derived class. Any class that tries to inherit this class won't have any access right to the protected fields of your base class (since the first inheritance changed the access right from `protected` to `private`.)
	- Basically, the [access right](C++%20Classes.md#Protection) defined here will determine what access right the public inherited fields in the base class will have. 


- Derived class inherits most members of base class, regardless of protection. They can only access `public` and `protected` 
- Derived class does not inherit
	- constructors
	- assignment operators if explicitly defined
- Derived class cannot delete things it inherited; cannot pick and choose what to inherit
- Derived class can **override** inherited member functions. 

## Inheritance and Constructor
Derived classes don't inherit constructors, but usually needs to call their base class constructor to initialize inherited data member. 
- Do this with the base class name in C++ (no `super()` like in Java).
- The base class constructor must be the first thing in the derived class constructor because if it is missing, then a default constructor for the base class will be called automatically; error if one doesn't exist. 

```c++
CheckingAccount(double initial, double atm) :
	Account(initial), total_fees(0.0), atm_fee(atm) { }
```
- When a derived class object is created, its inherited (base) parts must be initialized before any newly defined parts by executing a base constructor

## Inheritance and Destructor
When the lifetime of a derived object is about to end, two destructors are called: the one defined for the derived object, and the one defined for the base class.
- Destructor may be explicitly defined, or just provided the default
- A chain call happens for multi-level inheritance
- Constructors and destructors are executed in opposite orders!