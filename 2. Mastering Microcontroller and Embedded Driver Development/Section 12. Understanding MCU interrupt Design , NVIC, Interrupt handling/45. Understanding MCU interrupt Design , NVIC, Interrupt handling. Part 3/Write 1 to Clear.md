# чому ми маємо записувати "1" в Pending register (EXTI_PR), щоб очистити певний біт, якщо там уже 1 в момент interrupt?
Логіка запису `1`, щоб **очистити біт** у регістрі очікування (`EXTI_PR`), може здатися нелогічною на перший погляд. Але насправді це стандартний підхід у багатьох периферійних регістрах STM32.

---

## 🔹 **Чому запис "1" очищає біт у EXTI_PR?**
Регістр **EXTI_PR (Pending Register)** – це **"флаговий" регістр**. Його біти встановлюються в `1`, коли відбувається переривання на відповідному вході EXTI.  

ℹ️ **Але цей регістр працює не як звичайна пам'ять!** Запис `0` не має ефекту, а **запис "1" у певний біт скидає (очищає) його**.

### 🔥 **Причина – механізм "Write 1 to Clear" (W1C)**
- Біти цього регістру **автоматично виставляються в "1" при події переривання**.
- Щоб скинути їх назад у `0`, **процесор повинен записати "1" у відповідний біт**.
- Запис `0` не має ефекту – він просто ігнорується.

### 📌 **Що станеться, якщо записати "0"?**
👉 Нічого. Біт залишається `1`, і переривання може повторно спрацьовувати.

---

## 🔹 **Приклад коду (очищення EXTI_PR у STM32)**
Припустимо, у нас **переривання на EXTI_5**, і ми хочемо очистити прапор:

```c
EXTI->PR |= (1 << 5);  // Записуємо "1", щоб очистити біт 5
```
⏩ **Що тут відбувається?**  
- `EXTI->PR` має `1` у біті `5` (бо сталося переривання).
- Ми записуємо `1` у цей же біт.
- Контролер розуміє це як команду "очистити цей біт".
- Біт повертається в `0`, і флаг переривання скидається.

---

## 🔹 **Що буде, якщо не очистити біт EXTI_PR?**
🔴 **Переривання повторюватиметься нескінченно**!  
Оскільки біт `1` означає "переривання активне", воно буде знову і знову викликатися.

---

## 🔹 **Чому використовується саме такий підхід?**
1️⃣ **Безпека** – немає ризику випадково очистити інші біти.  
2️⃣ **Ефективність** – запис у регістр виконується одним `OR`-оператором.  
3️⃣ **Швидкість** – не потрібно додаткових операцій читання-запису.  

---

## 🔥 **Висновок**
✔ **Запис "1" у EXTI_PR очищає прапор переривання**.  
✔ **Це стандартний механізм "Write 1 to Clear" (W1C)** в STM32.  
✔ **Якщо цього не зробити – переривання буде повторюватися без зупинки**.  


# Ми по суті сигналізуємо процесору записати туди нуль, коли записуємо туди один?
Так, саме так! 🔥 Коли ми **записуємо "1"** в EXTI_PR, це означає, що **контролер самостійно змінює цей біт на "0"**. Тобто, ми не безпосередньо записуємо `0`, а **просимо процесор очистити біт**.  

Це працює завдяки механізму **"Write 1 to Clear" (W1C)**. Процесор "бачить" запис "1" і виконує внутрішню операцію очищення, яка скидає біт у `0`.

### 🔥 **Аналогія**
Уяви собі кнопку "Скинути помилку" на приладі:  
- Якщо світиться червона лампочка (`1`), це означає, що сталася помилка.  
- Ти натискаєш кнопку ("записуєш `1`"), і лампочка гасне (`0`).  

Те ж саме відбувається з EXTI_PR! 🚀