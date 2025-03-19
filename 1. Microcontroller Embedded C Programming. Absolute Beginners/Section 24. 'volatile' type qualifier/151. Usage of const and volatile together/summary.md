# Usage of `const` and `volatile` together
`pReg` is a pointer to a memory-mapped register. The `const` qualifier indicates that the pointer itself cannot be modified, while the `volatile` qualifier indicates that the value at the address pointed to by `pReg` can change at any time (e.g., due to hardware events).
```c
uint8_t volatile *const pReg = (uint8_t*) 0x40020000;
```

The `const` qualifier is applied to the pointer, meaning that the address stored in `pReg` cannot be changed **in the code** after initialization. The `volatile` qualifier is applied to the data type, indicating that the value at that address **may change unexpectedly (e.g., due to hardware events)**. This is also `const` pointer that cannot point to another address after initialization.
```c
uint8_t const volatile *const pReg = (uint8_t*) 0x40020000;
```

## Case of reading from read-only buffer or address which is prone to unexpected changes
```c
uint8_t const volatile *const pReg = (uint8_t*) 0x40020000;
```

This is input data register of a peripheral or a shared memory from which you are supposed to read-only.

Вказівники на реєстри з [попереднього прикладу](../148.%20Using%20volatile%20to%20fix%20issues%20with%20the%20pin-read%20exercise/summary.md) можна переписати наступним чином:
```c
uint32_t volatile * const pClkCtrlReg = (uint32_t *)0x40023830; // RCC, clock control register
uint32_t volatile * const pPortDModeReg = (uint32_t *)0x40020C00;
uint32_t volatile * const pPortDOutReg = (uint32_t *)0x40020C14;

uint32_t volatile * const pPortAModeReg = (uint32_t *)0x40020000;
uint32_t const volatile * const pPortAInReg = (uint32_t *)0x40020010; // Read-only register, mark it as const
```
