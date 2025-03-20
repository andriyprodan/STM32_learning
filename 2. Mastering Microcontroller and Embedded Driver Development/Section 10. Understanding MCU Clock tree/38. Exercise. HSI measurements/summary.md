# Exercise: HSI measurement
Write a program to output HSI clock on microcontroller pin and measure it using oscilloscope or logic analyzer.

## Steps to output a clock on MCU pin
1. Select the desired clock for the MCOx signal (Microcontroller Clock Output).
2. Output the MCOx signal on the MCU pin.

на схемі у вкладці **Clock configuration** є **MCO**. За замовчуванням він не активується, щоб його активувати, потрібно виконати наступні кроки:
- Перейти на вкладку **Pinout & Configuration**.
- У секції **System Core** обрати **RCC**.
- Поставити галочки біля **Master Clock Output 1** та **Master Clock Output 2**.

Важливо розуміти, що **MCO** - це сигнал всередині мікроконтролера і потрібно за допомогою коду перенаправити цей сигнал на пін. **MCO** можна використовувати як вхідний зовнішній сигнал для інших мікроконтролерів(HSE).

### Як це робиться за допомогою коду та регістрів?
Для плати **NUCLEO** знаходимо в мануалі регістр для активації годинників: **6. Reset and clock control(RCC) > RCC registers > 6.3.3 RCC clock configuration register(RCC_GFGR)**. Там є біти конфігурації для **MCO1**(біти 21 та 22). Залежно від значень цих бітів, на MCO приймається сигнал від різних джерел:
- 00: HSI clock selected
- 01: LSE clock selected
- 10: HSE clock selected
- 11: PLL clock selected

## Як перенаправити сигнал MCO на пін?
в [datasheet](https://www.st.com/resource/en/datasheet/stm32f446re.pdf) в розділі **4 Pinout and pin description > Table 11. Alternate function** вказано, що якщо *alternate function mode* встановлено як **AF0**, то сигнал MCO1 буде перенаправлено на пін **PA8**.  
**PA8** це 8й пін GPIO порту **A**. Щоб зрозуміти, якому піна на платі відповідає цей пін мікроконтролера, необхідно перейти в пункт **4 Pinout and pin description > Table 10. STM32F446xx pin and ball descriptions**. В табличці, в залежності від збірки плати (наприклад, LQFP64, WLCSP90 і т.д.), вказано, який пін мікроконтролера відповідає якому піну на платі.