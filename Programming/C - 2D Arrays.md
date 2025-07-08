---
tags:
  - programming
  - C
date: 2025-08-07
---
# 2D Arrays

- Arrays where each element is an array.
- Array of arrays.
- Good for matrices/grids of data.
## Syntax

- `array[][]` - declare 2D array
	- first bracket = row number (for grid) or array
	- second bracket = columns
	- must specify number of columns in second brackets
- `{{}, {}, {}};` - elements as part of the array
## Code Blocks

### Basic 2D Array

```c
int main() {    // main function

    int numbers[][3] = {{1,2,3}, {4,5,6}, {7,8,9}};   // 2D array

    printf("%d ", numbers[0][0]);   // prints 1
    printf("%d ", numbers[0][1]);   // prints 2
    printf("%d ", numbers[0][2]);   // prints 3

    return 0;

}
```
### Array Nested Loop

```c
int main() {    // main function

    int numbers[][3] = {{1,2,3}, {4,5,6}, {7,8,9}};   // 2D array

    for (int i =0; i <3; i++) {   // charge of rows
        for (int j =0; j <3; j++) {    // charge of columns
            printf("%d ", numbers[i][j]);
        }
        printf("\n");
    }
    
    return 0;

}
```