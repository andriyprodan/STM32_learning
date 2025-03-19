Створюємо проєкт в IDE "led_on"
- **AHB1ENR** - 0x4002 3830 (RCC, clock control register)
- **GPIOD_MODER** - 0x4002 0C00 (GPIOD, mode register)
- **GPIOD_ODR** - 0x4002 0C14 (GPIOD, output data register)
  
Ми використовуємо `uint32_t *` як тип вказівника, бо всього є $2^{32}$ бітів пам'яті (адрес), і ми можемо вказати на будь-яку з них. Назви вказівників починаємо з літери `p`, щоб вказати, що це вказівник.
```c
#include <stdint.h>

int main(void) {
    uint32_t *pClkCtrlReg = (uint32_t *)0x40023830;
    uint32_t *pPortDModeReg = (uint32_t *)0x40020C00;
    uint32_t *pPortDOutReg = (uint32_t *)0x40020C14;

    // 1. Enable the clock for GPIOD peripheral, set 3rd bit to 1 using bitwise OR
    // we use OR operation with 0x00000008 (0000 0000 0000 0000 0000 0000 0000 1000) mask to set 3rd bit to 1
    uint32_t temp = *pClkCtrlReg; // values (32 bits) in the register. pClkCtrlReg is pointing to the address of this value
    temp = temp | 0x08; // set 3rd bit to 1
    *pClkCtrlReg = temp; // write back to the register

    // instead you can do this:
    *pClkCtrlReg |= 0x08; // set 3rd bit to 1
    
    // 2. Configure the mode of the IO pin as output
    // we set 25th and 24th bit to 01 (25 - 0, 24 - 1) to configure pin 12 as output
    // a. Firstly we clear the 24th and 25th bits (set to zero)
    *pClkCtrlReg &= 0xFCFFFFFF; // CLEAR
    // b. Then set 24th bit to 1
    *pClkCtrlReg |= 0x01000000; // SET

    // 3. Set 12th bit of the output data register to make I/O pin-12 HIGH
    *pClkCtrlReg |= 0x1000; // set 12th bit to 1

    while (1);
}
```

Щоб подивиться значення різних регістрів необхідно натиснути **"Window > Show View > SFR"**. Блок регістрів з'явиться справа, там де debug значення. Там можна вибрати **GPIOD** і подивитися значення регістрів.


