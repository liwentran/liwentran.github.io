# Number Representations

## Integers: Two's Complement
When representing signed integers, we used a system named "two's complement".
In this system, we use the first three bits to represent the number, and the last bit represents the sign. `0` is postiive and `1` is negative. 

We use this two's complement system to represent integer numbers and types in C. 
### Properties
![](twos%20complement.png)
If you take any positive number in a two's complement system, flip the bits (take its complement) and add one, you will get the negative representation of that number. For example: take the complement of +3 (`0011`) to get `1100`. Add one to get `1101`. This is the binary represent for -3. 

When a two's complement number overflows, it wraps around to a negative number. If you are at maximum, +7 (`0111`), and you add one, it will over flow. If it overflows, it will wrap around to `1000`, which represents -8. If you subtract one from -8 (`1000`) it will wrap around to +7 (`0111`)

## Number Representation Differences
Integers and floating-point representations differ (the way we represent integers values is totally different from how we represent floating-point numbers ):
- Integers have limited range but integers in the range can be represented precisely. Floating point have limited range and can only approximate most numbers in the range. 
- Integers use all available bits for two's-complement representation. Floating point have separate sets of bits for sing, exponent, and mantissa. 

## Integer Literal Types
The type for an *integer literal* (e.g. `88`, `-1000000`) is determined based on its value. Its type is the smallest integer type that can store it without overflowing. 

## Floating-point Literal Types
*Floating-point literal* (e.g. `3.14`, `-.7`, `-1.1e-12`) has type `double`. Force it to be a `float` by adding f suffix:
```c
float a = 3.14f;
```

# Type Conversion
When you do `float a = 1` or `int i = 3.0`, it's not as simple as copying bits. The system of representation differs. 

When going from integer types to a `float` (or `double`) we are getting an approximation, not the exact integer. 

C can automatically convert between types "behind the scenes." There are two types of *automatic conversion*:
- *Promotion* (or *widening*) in the case of a smaller type value converted to a larger type. E.g. `float ten = 10;`.
- *Narrowing* in the case of a larger type value converted to a smaller type. E.g. `int ten = 10.585` (int <- double so it truncates to `10`).

### Promoting
```c
int a - 3;
float f = 1 * 1.5;
```
When operand types don't match, the "smaller" type is promoted to the "larger" type before applying an operator. The hierarchy is as follows:
`char` < `int`< `unsighed` < `long` < `float` < `double`

When the operand types do match, then it will be operated in that type. If it is assigned to a different type, then implicit type conversion occurs. 
```c
int a = 3;
float b = a/2; // b will store 1.00 
```

### Narrowing
Type conversion from larger to smaller types can also happen automatically (explicit type casts are not required). It's sometimes called *narrowing* conversions, and these chop off the extra bits without rounding values. 

A value's type is narrowed *automatically* and *without a compiler earning* when:
- assigning to a variable of narrower type
- passing an argument into a parameter of a narrower type.

Other narrowing situations yield compiler warnings, which can be eliminated by using explicit type casts.

### Casting
Some types just can't be used for certain things, like you can't use a float as an array index.

Type *casting* gives you more control over when promotion and narrowing happens in your program. 

Making explicit conversions can make your code clearer. 

Casing is a higher precedence operation than the binary arithmetic operator since it is a unary operator. 
