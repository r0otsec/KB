---
tags:
  - programming
  - C
date: 2025-08-07
---
# Array of Structs

- Array where each element contains a struct
- Helps organize and groups together related data
## Syntax

- `structName arrayName[] = { {structdata} }`
	- e.g. `Car cars[] = { {"Blah, 2025, 123} };`
## Code Block

### Car Array

```c
typedef struct {    // create car struct
    char model[25];
    int year;
    int price;
}Car;

int main() {

    Car cars[] = {{"Mustang", 2025, 32000},
                {"Corvette", 2026, 118000},
                {"Challenger", 2024 ,29000}};  // array of struct

    int number = sizeof(cars) / sizeof(cars[0]);

    for (int i = 0; i < number; i ++) {
        printf("%s %d $%d\n", cars[i].model, cars[i].year, cars[i].price);
    }

    return 0;

}
```