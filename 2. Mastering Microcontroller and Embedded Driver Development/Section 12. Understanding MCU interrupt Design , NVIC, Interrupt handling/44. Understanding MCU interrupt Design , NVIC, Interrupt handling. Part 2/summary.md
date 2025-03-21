Some peripherals deliver their interrupt to the NVIC over the EXTI line. Some peripherals deliver their interrupt directly to the NVIC.

В [reference manual](https://www.st.com/resource/en/reference_manual/rm0390-stm32f446xx-advanced-armbased-32bit-mcus-stmicroelectronics.pdf) **Interrupts and events > External interrupt/event controller (EXTI) > External interrupt/event line mapping** можна побачити, які піни відправляють сигнали переривання на які лінії EXTI.  
**Наприклад:** всі нульові піни GPIO(PA0, PB0, PC0...) відправляють сигнал на лінію EXTI0. Це означає, що можна використовувати **тільки один** з цих пінів для переривання одночасно серед усіх нульових пінів.  
Щоб визначити, з якого саме піна отримувати переривання, необхідно використовувати регістр **SYSCFG_EXTICR1** і там налаштовувати три біти для EXTI0. І потім ми маємо перевизначити handler функцію EXTI0 в коді, яка буде приймати сигнал переривання.

## Summary: Button interrupt
How does a button issue interrupt to the processor in STM32?
1. The button is connected to a GPIO pin of the microcontroller.
2. The GPIO pin should be configured to input mode
3. The link between a GPIO port and the relevant EXTI line must be established using the SYSCFG_EXTICRx register.
4. Configure the trigger detection (falling/rising/both) for relevant EXTI line (This is done via EXTI controller registers)
5. Implement the handler to service the interrupt