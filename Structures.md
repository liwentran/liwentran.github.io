# Structures

C is not an object oriented class, so there are no classes.

A *struct* is a collection of related variables, bundled together into one variable. That means there are no member functions. 

E.g., think about what you need in checkers. A checkers_piece would have the fields: x (horizontal offset), y (vertical offset), and black (0 = white, non-0 = black). 

## Syntax 
**Definition**
The `struct name { ... };` syntax defines a new struct data type. 
```c
struct date {
	int year;
	int month;
	int day;
}; 
```
The variables in a struct are called *fields*.  They can be other `structs`. 

**Declaration**
This syntax declares a *variable* that *has* that type:
```c
struct date today; 
```

**Initialization**
`struct` variable can be initialized in a similar way to an array:
```c
struct date today = (2021, 9, 28);
```

**Accessing fields**
Access the fields in a parameter:
```c
d.date = 1;
d.month++;
```

**Pointers as fields**
`struct` fields can be pointers as well, which is preferred because it is space efficient (pointers are only 8 bytes) and it allows updates to "propagate" to the `struct`.
```c
struct team {
	struct player *catcher;
	struct player *first_baseman;
	struct player *second_baseman;
}
```

**`sizeof()`**
`sizeof(struct player)` returns total size of all fields. (so `date` would be 12 bytes). 
The size of struct is *at least* the sum of the sizes of its fields. It can be bigger if the compiler decides to add "padding," which is extra space between fields. 

**Operators**
`d->day` is a synonym for `(*d).day`. This is preferred because there is a smaller number of operators. 

**Arrays**
You can have an array of `structs`:
```c
struct album music_collection[99999];
music_collection[0].name = "The Next Day";
music_collection[1].length = 41.9;
```
You can have a `struct` with an array in it:
```c
struct cc_receipt {
	char cc_number[16];
}
```

## Passing into a Function
A struct can be a function parameter and/or return type.
```c
struct date next_day(struct date d) {
	...
	return d;
}
```
A `struct` is a pass-by-value so we need to return a new `struct` or take a pointer to a `struct` and dereference/modify it. 

When a `struct` is passed to a function, everything inside is copied, including arrays. This means an array wrapped in a `struct` is a pass-by-value. 

## Typedef
We can get tired of writing `struct` over and over again, so we use this shorthand:
```c
typedef struct {
	float amount;
	char cc_number[16]; 
} cc_receipt; // we move the name to the end

cc_receipt lunch_receipt;
cc_receipt dinner_receipt;
```
Now we can refer to the type simply as `cc_receipt` instead of `struct cc_receipt`. 

## Nested structs
Structures can be nested:
```c
typedef struct {
	struct {
		int r;
		int b;
		int g;
	} color;
	struct {
		int x;
		int y;
	} position;
} pixel;

pixel p;
p.color.r = 255;
p.positon.x = 40; 
```
You can take out color and position and make them stand alone `structs` and then add `struct color c` into pixel. However, use this when you don't need them as stand along `structs`. 