# Data type size and compiler
Data types may cause portability issues of code when compiler changes.  
One compiler may consider integer data type size as 2 bytes, another compiler may consider it as 4 bytes and some other compiler may consider it as 8 bytes.

# `stdint.h`
To avoid this issue, C99 introduced a new header file `stdint.h` which defines exact width integer types.  
The standard library header file defines fixed-width integers using alias data types for the standard data types available in 'C'  
A fixed-width integer data type is an aliased data type that is based on the exact number of bits required to store the data.  

`stdint.h` helps you to choose an exact size for your variable and makes code portable no matter which compiler the code may be compiled on.  
Exact Alias | Description | range
--- | --- | ---
`int8_t` | exactly 8-bits signed | -128 to 127
`uint8_t` | exactly 8-bits unsigned | 0 to 255
`int16_t` | exactly 16-bits signed | -32768 to 32767
`uint16_t` | exactly 16-bits unsigned | 0 to 65535
`int32_t` | exactly 32-bits signed | -2147483648 to 2147483647
`uint32_t` | exactly 32-bits unsigned | 0 to 4294967295
`int64_t` | exactly 64-bits signed | -9223372036854775808 to 9223372036854775807
`uint64_t` | exactly 64-bits unsigned | 0 to 18446744073709551615

## Example
Here, doesn't matter under which compiler this code compiles, the compiler will always reserve 32 bits for the variable by using suitable standard data type.  
```c
#include <stdint.h>
int main() {
    uint32_t count=0;
    count++;
    if (count > 65536) {
        count = 0;
    }
    return 0;
}
```

# Some useful `stdint.h` aliases while programming
- `uintmax_t` - defines the largest fixed-width unsigned integer possible on the system.
- `intmax_t` - defines the largest fixed-width signed integer possible on the system.
- `uintptr_t` - defines an unsigned integer type that is wide enough to store the value of a pointer.