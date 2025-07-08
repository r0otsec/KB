---
tags:
  - programming
  - C
date: 2025-08-07
---
# Array Input

- User input can be stored in an array.
- Declared arrays must specify the size.
- Empty arrays include leftover data
	- C does NOT clear memory from programs.
## Syntax

- `int scores[5]` - initialize array with X elements
- `int scores[5] = {0}` - all elements set to 0
## Code Blocks

### Empty Array

```c
int main() {    // main function

    int scores[5] = {0};

    for (int i = 0; i < 5; i++) {
        printf("%d ", scores[i]);
    }

    return 0;

}
```
### For Loop Arrays

```c
int main() {    // main function

    int scores[5] = {0};

    for (int i = 0; i < 5; i++) {  // ask user for 5 numbers
        printf("Enter a score: ");
        scanf("%d", &scores[i]);   // enter data into array
    }

    for (int i = 0; i < 5; i++) {
        printf("%d ", scores[i]);
    }

    return 0;

}
```