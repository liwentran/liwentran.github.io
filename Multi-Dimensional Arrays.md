# Multi-Diemensional Arrays
## Declaration
- `<base_type> [dim1_sz][dim2_sz];`
- `<base_type> [dim1_sz][dim2_sz][dim3_sz];`
- `<base_type> [dim1_sz][dim2_sz][dim3_sz][dim4_sz];`

## Two-dimensional arrays
`int a[row_size][col_size]` is the declaration.
Example: `int table[2][4] = { {1,2,3,4},{5,6,7,8};`
![](Pasted%20image%2020210920142052.png)
- Physically in memory, laid out as one contiguous block of 2\*4=8 int sized locations.
- Array elements are stored in *row-major order* (all of `row1` comes first, then all of `row2`).
- `table` - holds address of first element of 2D array. 
- `table[i][j]` - referes to the `j`th element in `i`th row of 2D array.

2D arrays can also be [dynamically-allocated](Memory.md#Dynamically-allocated%20Two%20Dimensional%20Arrays).
## Multi-dimensional Arrays and Functions
When specifying multi-dimensional arrays as function parameters, you do not need to specify the first array size, but the second and following dimensions must be given.
```c
void sum_matrix(int list[][4], int numRows);
```