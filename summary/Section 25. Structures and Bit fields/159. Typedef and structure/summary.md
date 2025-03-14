# Typedef and structure
Typedef is used to give an alias name to primitive and user defined data types.

Замість того, щоб робити так:
```c
struct CarModel {
    unsigned int carNumber;
    uint32_t carPrice;
    uint32_t carMaxSpeed;
    float carWeight;
};

struct CarModel carBMW, carFord;
```
Ми можемо трохи скоротити код:
```c
typedef struct CarModel {
    unsigned int carNumber;
    uint32_t carPrice;
    uint32_t carMaxSpeed;
    float carWeight;
} CarModel_t;

CarModel_t carBMW, carFord; // більше не потрібно писати struct
```