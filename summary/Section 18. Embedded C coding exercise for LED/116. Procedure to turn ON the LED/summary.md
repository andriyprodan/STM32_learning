# Procedure to turn on the LED
1) Identify the GPIO port(a peripheral) used to connect the LED  
   **GPIOD**
2) Identify the GPIO pin where the LED is connected  
   **PD12**
3) Activate the GPIOD peripheral (Enable the clock)
   - Until you enable the clock for a peripheral, the peripheral is dead and it neither functions nor it takes any configuration values set by you.
   - Once you active the clock for a peripheral, the peripheral is ready to take your configuration and control-related commands or arguments (configuration values).
   - Note: For some microcontrollers, the peripheral may be ON by default, and you need not do any activation. (you should explore by the device datasheet for reference manual)
4) Configure the GPIO pin mode as output  
  Since you are driving an LED, the operation mode of the GPIO pin has to be configured as output.
5) Write to the GPIO pin
   1 (HIGH) to make the GPIO pin state HIGH(3.3V)
   0 (LOW) to make the GPIO pin state LOW(0V) 