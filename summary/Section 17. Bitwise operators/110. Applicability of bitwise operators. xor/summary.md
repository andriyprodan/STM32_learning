# Toggling of bits
Можна використовувати **XOR** для перемикання(toggle) стану LED. Якщо LED увімкнено, вона вимкнеться, і навпаки.  
`Led_state = Led_state ^ 1;`  
![alt text](<www.udemy.com_course_microcontroller-embedded-c-programming_learn_lecture_16552032 (8).png>)  
Тут видно, що при послідовному виконанні XOR над одним і тим самим числом і маскою `1`, результат буде змінюватися між 0 і 1.