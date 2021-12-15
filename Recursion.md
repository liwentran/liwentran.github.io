# Recursion
*Recursion* is another way to express repetition
- Can be more succint than loops, more elegant, but can have (potential downsides). 
- It works by dividing large problems into one or more smaller problems and then extending the solution to the smaller problem(s) to a solution for the large problem.

Implement recursion by having the function call *itself* using different arguments. A function calling itself is called a *recursive call*.

## When to Use Recursion
1. The smaller problem(s) ("subproblems") have the same form as the larger problem. Subproblems are solved recursively by making another call to the same method using different parameter values. This means arguments passed to a recursive call must describe a sub-problem that is *smaller* (simpler) than the overall problem. However, you want the subproblem(s) to be as large as possible to ensure that only a small amount of work is required to extend the solution to the subproblem(s) to be a solution to the overall problem.
2. There must be one or more instances of the problem that can be solved *without* recursion, known as the *base cases*.
3. All recursive calls must *make progress* towards a base case, so that the computation will eventually complete. Trying to solve the same problem recursively is an *infinite recursion*. 

Recursion is great or computation on inherently recusive structures (i.e., recursive data structures like trees). Or, "divide and conquer" algorithms (e.g., merge sort, quicksort). 

Avoid using deep recursion.
## Downsides
Every function call requires a *stack frame*. A stack frame is an area of memory where variables and temporary values for a function call are stored, as well as the *return address* indicating the code location where the function call will return to. Every recursive call creates a *new* stack frame. 
- The *call stack*, where stack frames are allocated, is limited in size.
- "Deep" recursion may fail because the call stack size is exceeded. 

## Tracing a Recursive Computation
```c
unsigned sum_1_to_n(unsigned n) { 
	if (n == 0) { // check base case
		return 0; 
	} 
	return sum_1_to_n(n - 1) + n; 
} 

int main(void) { 
	printf("%u\n", sum_1_to_n(2)); 
	return 0;
}
```
![](stacks.png)
Note: the maximum number of stack frames at the "deepest" point is proportional to the value of `n` passed to `sum_1_to_n` (number of numbers we wanted to sum together).

