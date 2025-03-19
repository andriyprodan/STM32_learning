Це продовження цього [прикладу](../../Section%2023.%20Optimization/145.%20Analyzing%20pin%20read%20exercise%20disassembly%20with%20O0%20and%20O2/summary.md).

Код ламається, при застосуванні оптимізації O2+.

Щоб цього не ставалося, ми позначаємо вказівник, що вказує на адресу регістру вводу GPIOA, як `volatile`. Це означає, що змінна може змінюватися зовнішніми факторами, тому компілятор не повинен оптимізувати її.

```c
//...
uint32_t volatile *pPortAInReg = (uint32_t *)0x40020010;
//...

while (1) {
    uint8_t pinStatus = (uint8_t)(*pPortAInReg & 0x1); // read the 0th bit

    if (pinStatus) {
        *pClkCtrlReg |= (1 << 12); // set 12th bit to 1
    } else {
        *pClkCtrlReg &= ~(1 << 12); // clear 12th bit

    }
}
``` 

Всі змінні, які вказують на пам'ять мікроконтролера можна позначити як `volatile`.
```c
uint32_t volatile *pClkCtrlReg = (uint32_t *)0x40023830; // RCC, clock control register
uint32_t volatile *pPortDModeReg = (uint32_t *)0x40020C00;
uint32_t volatile *pPortDOutReg = (uint32_t *)0x40020C14;

uint32_t volatile *pPortAModeReg = (uint32_t *)0x40020000;
uint32_t volatile *pPortAInReg = (uint32_t *)0x40020010;
```
