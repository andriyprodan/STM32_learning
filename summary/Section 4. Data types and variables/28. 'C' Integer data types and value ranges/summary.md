`C` **integer** data types, their storage sizes and value ranges:
Data Type | Memory size (bytes) | Value range (decimal)
--- | --- | --- | ---
signed char | 1 | -128 to 127 
unsigned char | 1 | 0 to 255 
short int | 2 | -32,768 to 32,767
unsigned short int | 2 | 0 to 65,535
int | 4 | -2,147,483,648 to 2,147,483,647
unsigned int | 4 | 0 to 4,294,967,295
long int | 8 | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
unsigned long int | 8 | 0 to 18,446,744,073,709,551,615
long long int | 8 | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
unsigned long long int | 8 | 0 to 18,446,744,073,709,551,615

в деяких компіляторах можуть бути інші розміри для цих типів даних. Наприклад, для `int` може бути 2 байти, для `long int` - 4 байти тощо

Ці типи даних мають завжди фіксований розмір в пам'яті, незалежно від компілятора:
**Short(signed or unsigned)** - 2 байти
**char(signed or unsigned)** - 1 байт
**long long(signed or unsigned)** - 8 байтів