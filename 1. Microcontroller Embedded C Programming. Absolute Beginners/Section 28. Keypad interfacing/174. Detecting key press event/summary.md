# Detecting key press event
When no key is pressed, C1, C2, C3, C4 reads HIGH.

**Code logic is next:** Scan for keys row by row one at a time.

![alt text](<www.udemy.com_course_microcontroller-embedded-c-programming_learn_lecture_16607164 (7).png>)  

Ми в нескінченному циклі подаємо LOW сигнал тільки на один з рядків в одну одиницю часу, тобто сигнал LOW послідовно чергується між рядками. Ми зчитуємо напругу з стовпців. Якщо ми натискаємо кнопку, то зчитується LOW напруга. Ми визначаємо, який з стовпців в цей момент був LOW, і таким чином визначаємо, яка кнопка була натиснута. Тобто в один момент часу, тільки на **одному** рядку і на **одному** стовпці одночасно можуть бути LOW.
