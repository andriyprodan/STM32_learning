## Range of float
**Storage size**: 4 bytes
**Precision**: up to 6 decimal places
**Value range**: $1.2 \times 10^{-38}$ to $3.4 \times 10^{38}$

## Range of double
**Storage size**: 8 bytes
**Precision**: up to 15 decimal places
**Value range**: $2.3 \times 10^{-308}$ to $1.7 \times 10^{308}$

## Приклад
```c
#include <stdio.h>

int main(void) {
    float number = 45.78976834578;
    printf("Number: %f\n", number); // Number: 45.789768. Обрізається до 6 знаків після коми
    
    double number2 = 45.78976834578;
    printf("Number2: %0.14lf\n", number2); // Number2: 45.78976834578000. Виводить 14 знаків після коми, як вказано в форматі prinf

    // Збереження заряду електрона
    float chargeE = -1.60217662e-19;
    printf("Charge of an electron: %f\n", chargeE); // Charge of an electron: -0.000000, такий результат виводиться через те, що це дуже мале число.
    printf("Charge of an electron: %e\n", chargeE); // Charge of an electron: -1.602177e-19. Дві цифри після коми втрачаються

    // Щоб цифра не втрачалась, необхідно використовувати double
    double chargeE2 = -1.60217662e-19;
    printf("Charge of an electron: %le\n", chargeE2); // Charge of an electron: -1.60217662e-19. Виводить 6 знаків після коми
    printf("Charge of an electron: %0.28lf\n", chargeE2); // Charge of an electron: -0.0000000000000000000000001602176620. Виводить 28 знаків після коми


    


    return 0;
}