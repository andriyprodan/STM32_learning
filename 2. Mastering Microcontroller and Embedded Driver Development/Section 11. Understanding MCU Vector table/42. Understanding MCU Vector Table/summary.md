# Vector table Details of the MCU
what is vector table?  
table of vectors (table of addresses or pointers)

what are vectors?  
direction(pointers or addresses)

addresses of what?  
addresses of exception handlers (system exceptions + interrupts (external exceptions))  
15 system exceptions + 240 interrupts

    Exception handlers is just a C functions. These functions can be redefined by the user.

Vector table can be found in the **reference manual of the microcontroller**.

## Vector table columns
**Приклад**: **reset handler** викликається перший коли відбувається перезавантаження (reset) мікроконтролера.
### priority
Число пріоритету обробника переривання. Вказує на те, наскільки важливий цей обробник переривання в порівнянні з іншими обробниками переривання. Чим менше число, тим вищий пріоритет. Наприклад, 0 - найвищий пріоритет, 1 - другий за важливістю і т.д.
### Type of priority
Тут є два типи пріоритету:
- **fixed**. Пріоритет не можна встановлювати вручну. Він фіксований. Вказується в мануалі мікроконтролера.
- **settable***. Пріоритет можна встановлювати вручну в коді.
### Address
Значення в цих адресах - це інші адреси функцій(а також їхні тіла), які будуть виконуватись при виникненні переривання. Це адреси функцій-обробників переривання.

Якщо ми перевизначаємо якийсь обробник переривання власною функцією, її адреса повинна зберігатися в адресі, що вказана в таблиці векторів для конкретного переривання.

**Як перевизначити функцію переривання?**
В основному коді, необхідно просто об'явити функцію, з таким же іменем, наприклад `I2C1_EV_IRQHandler()`, і реалізувати її.