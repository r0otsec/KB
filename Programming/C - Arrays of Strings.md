---
tags:
  - programming
  - C
date: 2025-08-07
---
# Arrays of String

- Pain in the ass.
- String = array of characters.
- Store more than one string using 2D array - two sets of indices
- Similar to 2d array of characters (conceptually):
	- 2D array - all data in contiguous blocks of memory
	- String array - each string can be at different memory locations
## Syntax

- `char fruit[][10]` - must declare max number of chars for each string
## Code Blocks

### Basic String Array

```c
int main() {    // main function

    char fruits[][10] = {"Apple", "Banana", "Coconut"};

    for (int i =0; i < 3; i ++) {
        printf("%s\n", fruits[i]);
    }

    return 0;

}
```
### String Array - SizeOf

```c
int main() {    // main function

    char fruits[][10] = {"Apple", "Banana", "Coconut"};
    int size = sizeof(fruits) / sizeof(fruits[0]);  // calculate size of array

    for (int i =0; i < size; i ++) {
        printf("%s\n", fruits[i]);
    }

    return 0;

}
```
### String Array - For Loop

```c
int main() {    // main function

    char names[4][25] = {0};   // empty array, hold 3 name, max size 25
    int rows = sizeof(names) / sizeof(names[0]);

    for (int i = 0; i < rows; i++) {  // dynamically calculate size of array
        printf("Enter a name: ");
        fgets(names[i], sizeof(names[i]), stdin);
        names[i][strlen(names[i]) - 1] = '\0';   // clear whitespace 
    }

    for (int i = 0; i < rows; i++) {
        printf("%s\n", names[i]);
    }

    return 0;

}
```