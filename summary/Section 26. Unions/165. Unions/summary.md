# unions
- A *union* is similar to a structure except that all of its members start at the same location in memory.
- A union variable can represent the value of only one of its members at a time.

# Difference between union and structure
    size of the union is equal to the size of its largest member.

```c
struct address {
    uint16_t shortAddr;
    uint32_t longAddr;
}; // using 8 bytes of memory
// 2 bytes for shortAddr, 2 bytes for padding and 4 bytes for longAddr

union address {
    uint16_t shortAddr;
    uint32_t longAddr;
}; // using 4 bytes of memory
// We store value of only one member at a time
```

    Use unions instead of structures to save memory when access to its member elements is **mutually exclusive(взаємовиключні)**


```c
#include <stdio.h>
#include <stdint.h>

union Address {
    uint16_t shortAddr;
    uint32_t longAddr;
};

int main(void) {
    union Address addr;

    addr.shortAddr = 0xABCD;
    addr.longAddr = 0xEEEECCCC; // this will overwrite the value of shortAddr

    printf("shortAddr: %#x\n", addr.shortAddr); // 0xCCCC, last 2 bytes of longAddr
    printf("longAddr: %#x\n", addr.longAddr); // 0xEEEECCCC

    getchar();

    return 0;
}
```