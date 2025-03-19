```c
#include <stdint.h>
#include <stdio.h>

void delay(void) {
    for (uint32_t i = 0; i < 300000; i++);
}

int main(void)
{
	//peripheral register addresses
	uint32_t volatile *const pGPIODModeReg  =  (uint32_t*)(0x40020C00);
	uint32_t volatile *const pInPutDataReg  =  (uint32_t*)(0x40020C00+0x10);
	uint32_t volatile *const pOutPutDataReg =  (uint32_t*)(0x40020C00+0x14);
	uint32_t volatile *const pClockCtrlReg  =  (uint32_t*)(0x40023800+0x30);
	uint32_t volatile *const pPullupDownReg =  (uint32_t*)(0x40020C00 + 0x0C);

    // 1. Enable the peripheral clock of GPIOD peripheral
    *pClockCtrlReg |= (1 << 3); // set 3rd bit to 1

    // 2. Configure PD0, PD1, PD2, PD3 as output (rows)
    *pGPIODModeReg &= ~(0xFF); // clear 0-7 bits
    *pGPIODModeReg |= 0x55; // set 0-7 bits to 01010101

    // 3. Configure PD8, PD9, PD10, PD11 as input (columns)
    *pGPIODModeReg &= ~(0xFF << 16); // clear 16-23 bits

    // 4. Enable internal pull-up resistors for PD8, PD9, PD10, PD11
    *pPullupDownReg &= ~(0xFF << 16); // clear 16-23 bits
    *pPullupDownReg |= (0x55 << 16); // set 16-23 bits to 01010101

    while(1) {
        // make all rows HIGH
        *pOutPutDataReg |= 0x0F; // set 0-3 bits to 1111

        // make R1 LOW (PD0)
        *pOutPutDataReg &= ~(1 << 0); // clear 0th bit

        // scan the columns
        // check C1(PD8) low or high (TEST using bitwise AND)
        if ((*pInPutDataReg & (1 << 8)) == 0) {
            // C1 is LOW
            delay();
            printf("1\n");
        }

        // check C2(PD9) low or high 
        if ((*pInPutDataReg & (1 << 9)) == 0) {
            // C2 is LOW
            delay();
            printf("2\n");
        }

        // check C3(PD10) low or high
        if ((*pInPutDataReg & (1 << 10)) == 0) {
            // C3 is LOW
            delay();
            printf("3\n");
        }

        // check C4(PD11) low or high
        if ((*pInPutDataReg & (1 << 11)) == 0) {
            // C4 is LOW
            delay();
            printf("A\n");
        }

        // make all rows HIGH
        *pOutPutDataReg |= 0x0F; // set 0-3 bits to 1111
        // make R2 LOW (PD1)
        *pOutPutDataReg &= ~(1 << 1); // clear 1th bit

        // scan the columns
        // check C1(PD8) low or high (TEST using bitwise AND)
        if ((*pInPutDataReg & (1 << 8)) == 0) {
            // C1 is LOW
            delay();
            printf("4\n");
        }

        // check C2(PD9) low or high 
        if ((*pInPutDataReg & (1 << 9)) == 0) {
            // C2 is LOW
            delay();
            printf("5\n");
        }

        // check C3(PD10) low or high
        if ((*pInPutDataReg & (1 << 10)) == 0) {
            // C3 is LOW
            delay();
            printf("6\n");
        }

        // check C4(PD11) low or high
        if ((*pInPutDataReg & (1 << 11)) == 0) {
            // C4 is LOW
            delay();
            printf("B\n");
        }

        // make all rows HIGH
        *pOutPutDataReg |= 0x0F; // set 0-3 bits to 1111
        // make R3 LOW (PD2)
        *pOutPutDataReg &= ~(1 << 2); // clear 2d bit

        // scan the columns
        // check C1(PD8) low or high (TEST using bitwise AND)
        if ((*pInPutDataReg & (1 << 8)) == 0) {
            // C1 is LOW
            delay();
            printf("7\n");
        }

        // check C2(PD9) low or high 
        if ((*pInPutDataReg & (1 << 9)) == 0) {
            // C2 is LOW
            delay();
            printf("8\n");
        }

        // check C3(PD10) low or high
        if ((*pInPutDataReg & (1 << 10)) == 0) {
            // C3 is LOW
            delay();
            printf("9\n");
        }

        // check C4(PD11) low or high
        if ((*pInPutDataReg & (1 << 11)) == 0) {
            // C4 is LOW
            delay();
            printf("C\n");
        }

        // make all rows HIGH
        *pOutPutDataReg |= 0x0F; // set 0-3 bits to 1111
        // make R4 LOW (PD3)
        *pOutPutDataReg &= ~(1 << 3); // clear 3d bit

        // scan the columns
        // check C1(PD8) low or high (TEST using bitwise AND)
        if ((*pInPutDataReg & (1 << 8)) == 0) {
            // C1 is LOW
            delay();
            printf("*\n");
        }

        // check C2(PD9) low or high 
        if ((*pInPutDataReg & (1 << 9)) == 0) {
            // C2 is LOW
            delay();
            printf("0\n");
        }

        // check C3(PD10) low or high
        if ((*pInPutDataReg & (1 << 10)) == 0) {
            // C3 is LOW
            delay();
            printf("#\n");
        }

        // check C4(PD11) low or high
        if ((*pInPutDataReg & (1 << 11)) == 0) {
            // C4 is LOW
            delay();
            printf("D\n");
        }
    }
}
```