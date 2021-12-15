# Control 

## Logical Operators
See all the operators [here](https://www.tutorialspoint.com/cprogramming/c_operators.htm). 
- `&&`is called the "Logical AND" operator. If both the operands are non-zero, then the condition becomes true. 
- `||` is called the "Logical OR" operator. If any of the two operands is non-zero, then the condition becomes true. 
- `!` is called the "Logical NOT" operator. It is used to reverse the logical state of its operand. If a condition is true, then Logical NOT operator will make it false. 

## Compound Assignments
- `+=`
- `-=`
- `*=`
- `/=`
- `%=`

## Increments and Decrements
There are pre-increments/decrements and post-increments/decrements. 
- `++` Increments the variable by 1
	- `++a` Increments, then uses the new value of `a` in the expression in which `b` resides.
	- `a++` Uses the current value of `a` in the expression in which `a` resides, then increments.
- `--` Decreases the variable by `.
  - `--a` Decrements, then uses the new value of `b` in the expression in which `b` resides. 
  - `b--` Uses the current value of `b` in the expression in which `b` resides, then decrements. 

Example:

```c
int a = 10;
printf("%d", a++); // prints 10

int b = 10;
printf("%d", --b); // prints 9 
```



## Decision-statement

### if and else statements
Suppose that `a` represents some boolean expression.
```c
if (a) {
	print f("a is true\n")
}
```
If `a` evaluates to true, then it will print "a is true." If it is false, then the body of the if statement is not executed.

```c
if (a) {
	printf("a is true\n")
} else {
	printf("a is false\n")
}
```

### Switch gates
Switch gates are less versatile than if statements, but can be cleaner and shorter. 
```c
switch (integer expr) {
  case c1: stmt1;	// execution starting point for c1
  case c2: stmt2;
    			 break;
  case c3: 
  case c4: stmt4; //executes stmt3, stmt4 and stmtlast for matches of c3 or c4. 
  default: stmtlast;
}
```

When you list switches together, then it becomes an OR statement. In the example above, c3 and c4 is  `c3 || c4`.

If you don't have the `break`, the program will keep reading more cases, slowing down the program. 

Its good practice to always have a `default` case. 



# Loops

```c
while (boolean expression) {statements}
```

Iterates >=0 times, as long as the boolean expression evaluates to true, the body of the while loop will execute. Iterates >=0 times.
- A comma can separate two statements within the while condition: `while (parse = fscanf(inFile, "%f%f", &p, &r), parse == 2)` or using a parentheses `while ((parse = fscanf(inFile, "%f%f", &p, &r) == 2)`.



```c
do {statements} while (boolean expression)
```

Iterates >=1. Will execute at least once because the statements will be executed first. Allows once, then more times as long as the boolean expression evaluates to true. 



```c
for(initialize; boolean exp; update) {stmts}
```

Initialize happens first and one time; usually declares & assigns the "index variable." Then, the boolean expression is evaluated, and if true, that the `stmts` are run. Right after, `update` is then run *often it increments the index variable (`i++`), and the boolean expression is checked once more. 

Iterates >= 0 times, as long as the boolean expression is true. 



```c
break
```

Immediately exits loop. It is not a good practice to use `break` inside any loops. 



```c
continue
```

Immediately proceeds to the next iteration of loop. It goes back up to check the boolean expression. 



Example:

```c
// for_example.c
#include <stdio.h>
int main() {
  for (int i= 0; i<10; i++) {
    printf("%d", i); 
  }
}
```

Will print 10 times, starting with `0` all the way to `9`. Once `i` reaches 10, `i<10` is not satisfied so the loop will end. 


A loop that reads in values until no more are available:

```c
// sum.c
#inlcude <stdio.h>

int main() {
  int sum = 0;
  int addend; // addend's value is undefiend to start
  
  // read as many integers as we can
  while (scanf("%d", &addend)==1) {
    //accumulate the sum of all numbers
    sum += addend; 
  }
  
  // output the sum
  printf("%d\n", sum);
  return 0; 
}
```

This program continues to scan when you press enter. To signal the end-of-input, press `Ctrl-D` (possibly twice). `Ctrl-D` returns DOF which is `-1`.

Note that `&addend` has an ampersand in front of the variable name when working with `scanf`.

`scanf` has a return value. It returns how many inputs were read successfully. The boolean statement basically works as long as you can successfully read one integer value from the user. 

However, you should use `while(scanf(...) != EOF)` if you want to keep asking for input. 

A less desirable way to write the same program is with a `break`:

```c
// sum.c
#inlcude <stdio.h>

int main() {
  int sum = 0;
  
  while (1) {
    int addend = 0;
    if(scanf("%d", &addend) != 1) {
      break; // immediately exit loop
    }
    sum += addend; 
  }  
  // output the sum
  printf("%d\n", sum);
  return 0; 
}
```

This loop is messier, harder to follow, and more prone to errors. 

