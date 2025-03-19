Файл `math.c` містить наступні функції:
```c
long long int math_mul(int n1, int n2) {
    return n1 * n2;
}

float math_div(int n1, int n2) {
    return n1 / n2;
}
```

Використання функцій у файлі `main.c`:
```c
#include "math.h" # прототипи функцій math.c знаходяться тут
#include <stdio.h>

int main() {
    // 0x0FFF1111 = 268374289
    // множення дає дуже велике число і тип даних integer не підходить для такого числа
    // в момент множення у функції, результат скорочується до 32 бітів і виходить неправильний результат
    printf("Mul: %I64x\n", math_mul(0x0FFF1111, 0x0FFF1111)); 

    printf("Div: %f\n", math_div(10, 3)); // 3. Автоматично скорочується до цілого числа

    return 0;
}
```

Для того, щоб функції працювали правильно, необхідно конвертувати (**typecasting**) одне з чисел до типу `long long int` (для множення). Щоб повертати правильний результат з division, необхідно конвертувати один з аргументів до типу `float`.:
```c
long long int math_mul(int n1, int n2) {
    return (long long int) n1 * n2;
}

float math_div(int n1, int n2) {
    return (float) n1 / n2;
}
```