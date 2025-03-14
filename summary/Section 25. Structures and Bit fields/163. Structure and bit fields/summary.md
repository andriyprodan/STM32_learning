# bit fields
Ми можемо оптимізувати використання пам'яті в [попередньому прикладі](../162.%20Structure%20exercise%20implementation/summary.md) за допомогою **bit fields**.

Ми даємо інструкцію компілятору використовувати тільки певну кількість бітів для зберігання різних змінних. Всі вони зберігаються в ділянці пам'яті розміром 32 біти (uint_32_t).

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