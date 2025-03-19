Щоб контролювати піни порта "D" використовується **GPIO D** всередині мікроконтролера.  
**GPIO D** also has set of registers which are used to control pin's mode, state and other functionalities. Software has to write to these registers to control the pins. Also you can read data from the port.   
Each register has its own memory address. You can access the registers of this peripheral using memory addresses.

## Memory mapped I/O
- IO pins are controlled using peripheral registers which are mapped on to processor addressable memory locations.
- What are processor addressable memory locations? See in the next lecture