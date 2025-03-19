# 4x4 keypad interfacing
If you want to reproduce this project you would need
- 1 4x4 matrix keypad
- Few jumper wires to do the connection

Write a program which detects and prints the key pressed.

## Як працює матриця клавіатури
![alt text](<www.udemy.com_course_microcontroller-embedded-c-programming_learn_lecture_16607164 (2).png>)   
Мікроконтролер подає напругу (не обов'язково HIGH, може бути і LOW(GND)) на 4 рядки (row) та зчитує напругу з 4 стовпців (column). Коли ми натискаємо клавішу, то замикається контакт між рядком та стовпцем. Таким чином, ми можемо дізнатися, яка клавіша була натиснута.

## Схема підключення до STM32
![alt text](<www.udemy.com_course_microcontroller-embedded-c-programming_learn_lecture_16607164 (4).png>)
Нам потрібно використовувати 8 пінів мікроконтролера для підключення до матриці. pull-up резистори, що вказані на рисунку - це внутрішні резистори мікроконтролера. 