---
tags:
  - programming
  - C
date: 2025-08-07
---
# realloc()

- (Re)(Alloc)ation
- Resizes previous allocated memory
## Syntax

- `realloc()`
- Takes two arguments - `ptr` (pointer to old memory), `bytes` (new size) 
	- e.g. `realloc(ptr, bytes)`
 - Requires `#include <stdlib.h>`
- Common convention to create pointer named `temp` for realloc()
- `realloc()` needs pointer and bytes
	- copies prices over to new memory
	- e.g. `float *temp = realloc(prices, newNum * sizeof(float));`
		- returns pointer to new memory and copy previous values over
		- also `free()` old memory by default
## Code Blocks

### Realloc Example

```c
int main() {

    int num = 0;
    printf("Enter the number of prices: ");
    scanf("%d", &num);  // store at address of num var

    float *prices = malloc(num * sizeof(float));

    // check if mem alloc fails
    if (prices == NULL) {   
        printf("Memory allocation failed!");
        return 1;
    }

    for (int i = 0; i < num; i++) {
        printf("Enter price#%d: ", i + 1);   // user input
        scanf("%f", &prices[i]);  // store float at addr of pointer
    }

    int newNum = 0;
    printf("Enter a new number of prices: ");
    scanf("%d", &newNum);

    float *temp = realloc(prices, newNum * sizeof(float));

    if (temp == NULL) {
        printf("Could not rellocate new memory\n");
    }
    else {
        prices = temp;  // prices points at new memory rather than old
        //temp = NULL;  // useful if planning to reuse 

        for (int i = num; i < newNum; i++) {
            printf("Enter price#%d: ", i + 1);
            scanf("%f", &prices[i]);  
        }

        for (int i = 0; i < newNum; i++) {
            printf("$%.2f ", prices[i]);
        }

    }

    free(prices);  // free memory
    prices = NULL;  // reset pointer

    return 0;

}
```