This is modified code from the [previous exercise](../../Section%2019.%20Bitwise%20shift%20operators/123.%20Modifying%20LED%20on%20exercise%20using%20bitwise%20shift%20operators/summary.md)

```c
#include <stdint.h>

int main(void) {
    uint32_t *pClkCtrlReg = (uint32_t *)0x40023830;
    uint32_t *pPortDModeReg = (uint32_t *)0x40020C00;
    uint32_t *pPortDOutReg = (uint32_t *)0x40020C14;

    // 1. Enable the clock for GPIOD peripheral, set 3rd bit to 1
    *pClkCtrlReg |= (1 << 3); // стало
    
    // 2. Configure the mode of the IO pin as output
    // a. Firstly we clear the 24th and 25th bits (set to zero)
    *pClkCtrlReg &= ~(1 << 24); // CLEAR
    *pClkCtrlReg &= ~(1 << 25); // CLEAR
    // OR
    *pClkCtrlReg &= ~(3 << 24); // 3 is 11 in binary, we push ~(11)==00 to the left by 24 positions
    // b. Then set 24th bit to 1
    *pClkCtrlReg |= (1 << 24); // SET

    // 3. Set 12th bit of the output data register to make I/O pin-12 HIGH
    *pClkCtrlReg |= (1 << 12); // set 12th bit to 1

    // toggle LED using software delay
    while (1) {
        *pPortDOutReg |= (1 << 12); // set 12th bit to 1
        for (uint32_t i = 0; i < 500000; i++);
        *pPortDOutReg &= ~(1 << 12); // clear 12th bit
        for (uint32_t i = 0; i < 500000; i++);
    }
}
```