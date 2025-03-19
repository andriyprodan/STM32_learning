# Bitwise right shift operator(>>)
- This operator takes 2 operands
- Bits of the 1st operand will be right shifted by the amount decided by the 2nd operand
- Syntax: `operand1 >> operand2`

## Example
```c
char a = 111;
char b = a >> 4;
```
`a` in binary is `0110 1111`. We move the bits to the right by 4 positions, at the start we fill the empty positions with 0. So, `b` will be `0000 0110` which is 6 in decimal.