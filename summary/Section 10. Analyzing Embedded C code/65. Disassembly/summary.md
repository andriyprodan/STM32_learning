# Disassembly
Disassembly - це перегляд assembly коду, в який буд конвертований наш c код.

## Як скористатися функцією disassembly?
В режимі дебагу коду, натискаємо в треї `Window -> Show View -> Disassembly`. Відкриється вікно з асемблерним кодом, який відповідає нашому C коду.

### Disassembly використовуючи `objdump`
```bash
arm-none-eabi-objdump.exe -d <file>.elf
```

## Для чого потрібно використовувати disassembly?
Ми можемо використовувати функцію дебагу для відлагодження коду assembly, можна ставити breakpoints на кожній інструкії assembly.