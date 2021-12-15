# Bitwise

## Bitwise Operator
A bitwise operator performs a function across all bits in its operands. 
### Bit AND
Description: The bits in the result are set to 1 if the corresponding bits in the two operands are both 1. 

Bitwise AND (`&`) performs logical AND (`&&`) across all bits:
12 = 00001100 (in binary) and 25 = 000110001. The bit AND operation of 12 and 25 would be:
```
  00001100
& 00011001
__________
  00001000 = 8 (in decimals)
```


### Bit inclusive OR
Description: The bits in the results are set to 1 if at least one of the corresponding bits in the two operands is 1.

Bitwise OR (`|`) performs logical OR (`||`) across all bits.
12 = 00001100 (in binary) and 25 = 000110001. The bit OR operation of 12 and 25 would be:
```
  00001100
& 00011001
__________
  00011101 = 29 (in decimals)
```

### Bit exclusive OR
Exclusive OR (`^`).
Description: The bits in the results are set to 1 if exactly one of the corresponding bits in the two operands is 1. 

### Bit Shifting
Description: Shifts the bits of the first operand left (respectively right) by the number of bits specified by the second operand; fill from the right with 0 bits (respectively filling from the left is machine dependent).

`x << n` shifts bits of `x` to the left `N` positions.
`N` 0s are "shifted in" at right-hand side and `N` bits "fall off" left-hand side.
25 = 00011001 (in binary). The bitwise left-shift of 25 by 5 positions `(25 << 5)` would be 1100100000 = 800 (in decimals)

Similar for bitwise right shift (`>>`). 
Bitwise right shfit of 25 by four positions `(25 >> 4)` would be. 00000001 = 1 (in decimals).

### One's Complement
Description: All 0 bits are set to 1 and all 1 bits are set to 0. 