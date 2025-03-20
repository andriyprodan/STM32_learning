
# Exercise: HSE measurement (NUCLEO board)
1. Enable the HSEBYP bit (**RCC_CR**) (bypass the oscillator with an external clock)
2. Enable the HSE clock using HSEON bit (**RCC_CR**)
3. Switch the systemclock to HSE
4. Do MCO1 settings to measure it

# Exercise: HSE measurement (Discovery board)
Write a program to switch HSE as system clock and measure it

1. Enable th HSE clock using HSEON bit (**RCC_CR**)
2. Wait until HSE clock from external crystal stabilizes(only if crystal is connected, crystal is present on DISCOVERY boards)(indicates if the high-speed external oscillator is stable or not).
3. Switch thy system clock to HSE (**RCC_CFGR**).  
   **In RCC_CFGR:**  
   Bits 1:0 **SW**: System clock switch  
    - 00: HSI oscillator selected as system clock
    - 01: HSE oscillator selected as system clock
    - 10: PLL selected as system clock
    - 11: Not applicable
4. Do MCO1 settings to measure it

```c
#include <stdint.h>

#define RCC_BASE_ADDR 0x40023800UL

#define RCC_CFGR_REG_OFFSET 0x08UL

#define RCC_CR_REG_OFFSET 0x00UL

#define RCC_CFGR_REG_ADDR (RCC_BASE_ADDR + RCC_CFGR_REG_OFFSET)

#define RCC_CR_REG_ADDR (RCC_BASE_ADDR + RCC_CR_REG_OFFSET)

#define GPIOA_BASE_ADDR 0x40020000UL

int main(void) {
    uint32_t *pRccCrReg = (uint32_t *)RCC_CR_REG_ADDR;
    uint32_t *pRccCfgrReg = (uint32_t *)RCC_CFGR_REG_ADDR;
    // 1. Enable the HSE clock using HSE ON bit (RCC_CR)
    *pRccCrReg |= (1 << 16); // Set bit 16 to 1 (HSEON)
    // 2. Wait until HSE clock from external crystal stabilizes
    // We have to wait until Bit 17 (HSERDY) is set to 1 is the RCC_CR register
    while (!(*pRccCrReg & (1 << 17)));
    // 3. Switch the system clock to HSE (RCC_CFGR)
    *pRccCfgrReg &= ~(0x3); // Clear bits 1 and 0
    *pRccCfgrReg |= (1 << 0); // Set bits 1 and 0 to 01 (HSE selected as system clock)
    // 4. Configure the RCC_CFGR MCO1 bit fields to select HSE as clock source

    // 1) Configure the RCC_CFGR MCO1 bit fields to select HSE as clock source
    *pRccCfgrReg &= ~(0x3 << 21); // Clear bits 22 and 21
    *pRccCfgrReg |= (0x2 << 21); // Set bits 22 and 21 to 10 (HSE selected as MCO1 clock source)

    // Configure MCO1 prescaler
    *pRccCfgrReg &= ~(0x7 << 24);
    *pRccCfgrReg |= (1 << 26); 
    *pRccCfgrReg |= (1 << 25); 

    // 2) Configure PA8 to AF0 mode to behave as MCO1 signal
    // PA8 належить до GPIOA, тому потрібно активувати тактування GPIOA

    // a) Enable the peripheral clock for GPIOA peripheral
    uint32_t *pRccAhb1enrReg = (uint32_t *)(RCC_BASE_ADDR + 0x30UL);
    *pRccAhb1enrReg |= (1 << 0); // Enable GPIOA clock

    // b) Configure PA8 as alternate function mode
    uint32_t *pGpioaModerReg = (uint32_t *)(0x40020000UL + 0x00UL);
    *pGpioaModeReg &= ~(0x3 << 16); // Clear bits 16 and 17
    *pGpioaModeReg |= (0x2 << 16); // Set bits 16 and 17 to 10 (alternate function mode)

    // c) Configure the alternation function register to set the mode 0 for PA8
    uint32_t *pGPIOAAltFunHighReg = (uint32_t *)(0x40020000UL + 0x24UL);
    *pGPIOAAltFunHighReg &= ~(0xF << 0); // Clear bits 0 to 3


    for (;;);
}
```