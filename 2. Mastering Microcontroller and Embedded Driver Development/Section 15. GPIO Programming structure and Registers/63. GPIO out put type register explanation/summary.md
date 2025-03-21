# GPIO output type register
When a GPIO pin is in the output mode, this registter is used to select the output type of that pin.  
Output types:
- **push-pull**
- **open-drain**
  
Цей регістр має 16 бітів (на кожен порт GPIO), які можна встановлювати. 0 - це push-pull, 1 - open-drain.