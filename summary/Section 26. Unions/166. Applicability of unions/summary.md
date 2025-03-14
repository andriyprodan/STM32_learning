# Applicability of unions in Embedded System code
1. Bit extraction
2. Storing mutually exclusive data thus saving memory

## Example
```c
#include <stdio.h>
#include <stdint.h>

struct Packet {
    // all these variables will be referring to different bit fields of single uint32_t memory (4 bytes only)
    uint32_t crc        :2;
    uint32_t status     :1;
    uint32_t payload    :12;
    uint32_t bat        :3;
    uint32_t sensor     :3;
    uint32_t longAddr   :8;
    uint32_t shortAddr  :2;
    uint32_t addrMode   :1;
};

int main(void) {
    uint32_t packetValue;
    printf("Enter the 32bit packet value: ");
    scanf("%x", &packetValue);
    struct Packet packet;

    packet.crc = uint8_t (packetValue & 0x3); // останні 2 біти
    packet.status = uint8_t ((packetValue >> 2) & 0x1); // наступний 1 біт, попередні 2 ігноруються за допомогою оператора bitwise right shift
    packet.payload = uint16_t ((packetValue >> 3) & 0xFFF); // наступні 12 біт, попередні 3 ігноруються
    packet.bat = uint8_t ((packetValue >> 15) & 0x7); // наступні 3 біти, попередні 15 ігноруються
    packet.sensor = uint8_t ((packetValue >> 18) & 0x7); // наступні 3 біти, попередні 18 ігноруються
    packet.longAddr = uint8_t ((packetValue >> 21) & 0xFF); // наступні 8 біт, попередні 21 ігноруються
    packet.shortAddr = uint8_t ((packetValue >> 29) & 0x3); // наступні 2 біти, попередні 29 ігноруються
    packet.addrMode = uint8_t ((packetValue >> 31) & 0x1); // останній біт, попередні 31 ігноруються

    printf("crc: %#x\n", packet.crc);
    printf("status: %#x\n", packet.status);
    printf("payload: %#x\n", packet.payload);
    printf("bat: %#x\n", packet.bat);
    printf("sensor: %#x\n", packet.sensor);
    printf("longAddr: %#x\n", packet.longAddr);
    printf("shortAddr: %#x\n", packet.shortAddr);
    printf("addrMode: %#x\n", packet.addrMode);
    
    printf("Size of struct is % I64u\n", sizeof(packet));// виводить розмір структури в байтах. Виводить "4" байт
    // розмір пакета, який вводить користувач дорівнює 4 байти, тобто ми не витрачаємо пам'яті.

}
```

Ми можемо скоротити код, де дані дістаються із пакету і зберігаються в структурі, за допомогою комбінації `structure` і `union`.
```c
union Packet {
    uint32_t packetValue;
    struct {
        uint32_t crc        :2;
        uint32_t status     :1;
        uint32_t payload    :12;
        uint32_t bat        :3;
        uint32_t sensor     :3;
        uint32_t longAddr   :8;
        uint32_t shortAddr  :2;
        uint32_t addrMode   :1;
    } packetFields;
};
```

По суті `packetValue` і `packetFields` зберігаються в одній і тій же пам'яті. Коли ми присвоюємо значення `packetValue`, то всі поля структури `packetFields` автоматично заповнюються. І навпаки, якщо ми присвоюємо значення полям структури, то `packetValue` також заповнюється.
```c
int main(void) {
    union Packet packet;
    printf("Enter the 32bit packet value: ");
    scanf("%x", &packet.packetValue);

    // старий код не потрібен

    printf("crc: %#x\n", packet.packetFields.crc);
    printf("status: %#x\n", packet.packetFields.status);
    printf("payload: %#x\n", packet.packetFields.payload);
    printf("bat: %#x\n", packet.packetFields.bat);
    printf("sensor: %#x\n", packet.packetFields.sensor);
    printf("longAddr: %#x\n", packet.packetFields.longAddr);
    printf("shortAddr: %#x\n", packet.packetFields.shortAddr);
    printf("addrMode: %#x\n", packet.packetFields.addrMode);

    printf("Size of struct is % I64u\n", sizeof(packet));// виводить розмір структури в байтах. Виводить "4" байт


}