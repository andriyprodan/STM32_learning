Створюємо новий проєкт. У вкладці **Targeted Project Type** обираємо **Empty**.

**Суть проєкту**: Вивести сигнал HSI на пін **PA8**.

```c
#include <stdint.h>

#define RCC_BASE_ADDR 0x40023800UL

#define RCC_CFGR_REG_OFFSET 0x08UL

#define RCC_CFGR_REG_ADDR (RCC_BASE_ADDR + RCC_CFGR_REG_OFFSET)

int main(void) {
    uint32_t *pRccCfgrReg = (uint32_t *)RCC_CFGR_REG_ADDR;

    // 1. Configure the RCC_CFGR MCO1 bit fields to select HSI as clock source
    *pRccCfgrReg &= ~(0x3 << 21); // Clear bits 21 and 22

    // 2. Configure PA8 to AF0 mode to behave as MCO1 signal
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

    for(;;);
}
```

## Зміна prescaler MCO1 для зміни частоти HSI
prescaler змінюється в регістрі **RCC_CFGR**. Для цього потрібно змінити біти 26-24. В мануалі вказано, що якщо значення цих бітів:
- 0xx: no prescaler
- 100: division by 2
- 101: division by 3
- 110: division by 4
- 111: division by 5

```c
// Configure MCO1 prescaler
*pRccCfgrReg &= ~(0x7 << 24); // Clear bits 26 to 24
*pRccCfgrReg |= (1 << 26); // Set bits 26 to 24 to 100 (division by 2)
*pRccCfgrReg |= (1 << 25); // Set bit 25 to 1. 26-24 is now 110 (division by 4)
```