# When to use `volatile` qualifier?
- A variable must be declared using a volatile qualifier when there is a possibility of unexpected changes in the variable value.
- The unexpected changes in the variable value may happen from within the code or from outside the code (from the hardware).

Use volatile when your code is dealing with below scenarios:
1. **Memory-mapped peripheral registers** of the microcontrollers.
2. Multiple tasks accessing global variables(read/write) in an RTOS (Real-Time Operating System) multithreaded application.
3. When a global variable is used to share data between the main code and an ISR(Interrupt Service Routine) code.

## Case 2: non-volatile pointer to volatile data
```c
uint8_t volatile *pStatusReg;
```

`pStatusReg` is a non-volatile pointer, pointing to volatile data of type `unsigned integer_i`

**Use case:**  
This is a perfect case of accessing memory-mapped registers. Use this syntax generously whenever you are accessing memory mapped register in your microcontroller code.

## Case 3: volatile pointer to non-volatile data
```c
uint8_t * volatile pStatusReg;
```

## Case 4: volatile pointer to volatile data
```c
uint8_t volatile * volatile pStatusReg;
```

Case 3 and Case 4 are not very common in embedded systems programming. But you may come across them in some specific scenarios.