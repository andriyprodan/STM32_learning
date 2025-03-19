# Exercise
Create a structure named "CarDetails" which comprises below information
1) Car max speed        (Max 400 Km/hr) (7 bits)
2) Car weight in Kg     (Max 5000 Kg) (13 bits)
3) Car color            (an ASCII code of color) (7 bits)
4) Car price in USD     (Max 100,000,000 USD) (28 bits)

1. Structure without bit fields
   ```c
   struct CarDetails {
        uint16_t speed;
        uint16_t weight;
        char colour;
        uint32_t price;
   }; // 4 + 4 + 4 = 12 bytes
   ```

2. Structure with bit fields
   ```c
   struct CarDetails {
    // first 32 bits
    uint32_t speed      :7;
    uint32_t weight     :13;
    uint32_t colour     :7;
    // 27 bits are used, still 5 bits are left in this 32 bit memory
    uint32_t price_l    :5; // we store the lower 5 bits of price in the remaining 5 bits
    
    // next 32 bits
    uint32_t price_h    :23; // we store the higher 23 bits of price in the next 32 bit memory

    // but we can also store the price like this, that is also valid:
    // uint32_t price   :28; 

   }; // 4 + 4 = 8 bytes
   ```