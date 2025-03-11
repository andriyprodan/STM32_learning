# Bitwise left shift operator(<<)
- This operator takes 2 operands
- Bits of the 1st operand will be right shifted by the amount decided by the 2nd operand
- Syntax: `operand1 << operand2`

## Example
```c
char a = 111;
char b = a << 4;
```

`a` in binary is `0110 1111`. We move the bits to the left by 4 positions, at the end we fill the empty positions with 0. So, `b` will be `1111 0000` which is 240 in decimal.


# << vs >>
A value will be multiplied by 2 for each left shift.  
A value will be divide by 2 for each right shift.

<< (left shift) | >> (right shift)
--- | ---
$4 << 0 => 4$ | $128 >> 0 => 128$
$4 << 1 => 8$ | $128 >> 1 => 64$
$4 << 2 => 16$ | $128 >> 2 => 32$
$4 << 3 => 32$ | $128 >> 3 => 16$
$4 << 4 => 64$ | $128 >> 4 => 8$
$4 << 5 => 128$ | $128 >> 5 => 4$
