# Exercise
- Write a program which reads the status of the pin PA0. If the status of PA0 is LOW then turn off the on board LED(PD12) and if the status of PA0 is HIGH then turn on the LED.
- Change the status of PA0 pin manually by connecting PA0 to GND or VDD points of the board.

Перед тим, як використовувати PA0, необхідно подивиться в мануалі для плати, чи не зайнятий цей пін якоюсь внутрішньою електронікою. Якщо він не зайнятий, його можна використовувати як GPIO(genereal purpose input output) пін.

Ми можемо подивиться в табличці **STM32 pin description versus board functions**. В колонці **Free I/O** вказано, чи цей пін вільний для використання.

# Some hints
- PA0 should be in input mode
- To read from pin PA0, your code has to read PORT-A input data register