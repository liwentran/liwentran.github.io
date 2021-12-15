# Enumeration
An enumeration is a distinct type whose value is restricted to a range of values.
- An enum can include several explicitly named constants ("enumerators").
- The values of the constant are "integer" numbers.
- It is compiler-dependent to determine an "integer" type that can represent all enumerators. 

\
We use enumeration type because it can be more comprehensive and readable. 

## Example:
```c++
enum Color {red, green, blue}; // an unscoped enum

Color r = red;
switch (r) {
	case red: ...
	case green: ...
	case blue: ...
}
```

## Underlying type
Specify the underlying type:
```c++
enum class Color : char {red, yello, green=20, blue};
```

## Unscoped
```c++
enum Foo {a, b, c=10, d, e=1, f, g=f+c}
// a=0, b=1, c=10, d=11, e=1, f=2, g=12
```

- each enumerator is associated with a value of the underlying type. 

```c++
int num = c // c is 10
```
- the values can be converted to their underlying type (implicitly).

## Scoped
Declaring a scoped enumeration type whose underlying type is `int` (the keywords `class` and `struct` are exactly equivalent)

```c++
enum struct|class name {enumerator = constexpr, enumerator = constexpr , ...}
```

\
For example,
```c++
enum class Color { red, green=20, blue};
Color r = Color::blue;
```
The values can also be converted to their underlying type but explicitly:
```c++
int n = Color::blue; // NOT OK
int m = (int) Color::blue; // OK
int l = static_cast<int>(Color::blue) // OK
```


## Unscoped vs scoped
Unscoped enum type could be misused:
```c++
enum Color { red, yellow, blue };
enum MyColor { myblue, myyellow, myred };

Color col = red;
if (col == myred) { // should this be true?
}
```
- `Color` shouldn't be compared with `MyColor`. You will see a compiler warning, but the expression is allowed (because implicitly converted to the underlying type).
- Use scoped enum to avboid this.
