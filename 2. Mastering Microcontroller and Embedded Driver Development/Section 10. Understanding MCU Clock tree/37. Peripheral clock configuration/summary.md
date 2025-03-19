# Peripheral Clock configuration
- In modern MCUs, before using any peripheral, you must enable its peripheral clock using peripheral clock registers
- By default, peripheral clocks of almost all peripherals will be disabled to save power
- A peripheral won't take or respond to your configuration values until you enable its peripheral clock
- In STM32 microcontrollers, peripheral clocks are managed through RCC registers.

## RCC
**RCC** is a internal system related peripheral of the microcontroller. It is used for reset and clock control.