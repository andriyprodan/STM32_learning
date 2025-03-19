Для роботи мікроконтролера необхідно, щоб він мав тактовий сигнал. Тактовий сигнал - це періодичний сигнал (чергування HIGH-LOW з певним періодом), який використовується для синхронізації роботи мікроконтролера.

## Clocks
Three different clock sources can be used to drive the system clock (SYSCLK):
- HSE (high speed external) oscillator clock (Crystal oscillator, MCU external oscillator)
- HSI (high speed internal) oscillator clock (The RC (resistive and capacitive circuit) oscillator, MCU internal oscillator)
- Main PLL clock (Phase-locked loop, MCU internal)
