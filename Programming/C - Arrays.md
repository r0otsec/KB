---
tags:
  - programming
  - C
date: 2025-08-07
---
# Arrays

- Fixed size collection of elements of same data type.
- Like variables, but holds more than 1 value.
- Passing arrays to functions will decay into a pointer.
## Syntax

- Declared via `[]` after variable name
- Values included within `{}`
	- e.g. `int numbers[] = {1,2,3,4,5}`
- Must print element in array (each value):
	- e.g. `printf("%d", numbers[0])`
- Change element value:
	- `arrayName[0] = 100;`
- Display all elements of array using loops.
- Can calculate automatically size of array via `sizeOf()`
	- e.g. `printf("%d", sizeof(numbers))` - returns number of bytes
	- e.g. `printf("%d", sizeof(numbers[0]))` - returns size of element 1
## Code Blocks

### Basic Number Array

```c
int main() {    // main function

    int numbers[] = {10,20,30,40,50};   // array
    printf("%d", numbers[0]);  // print first element

    return 0;
    
}
```
### Basic Char Array

```c
int main() {    // main function

    int numbers[] = {10,20,30,40,50};   // array
    char grades[] = {'A','B','C','D','F'};  // array of chars

    printf("%c", grades[0]);  // print first element
    return 0;

}
```
### Basic String Array

```c
int main() {    // main function

    char name[] = "Jonny Pake";

    printf("%c", name[0]);  // print first char (J)
    return 0;

}
```
### Change Array Values

```c
int main() {    // main function

    int numbers[] = {10,20,30,40,50};   // array

    numbers[0] = 100;
    numbers[1] = 90;
    numbers[2] = 80;
    numbers[3] = 70;
    numbers[4] = 60;

    printf("%d\n", numbers[0]);  // print element
    printf("%d\n", numbers[1]);  // print element
    printf("%d\n", numbers[2]);  // print element
    printf("%d\n", numbers[3]);  // print element
    printf("%d\n", numbers[4]);  // print element
    return 0;

}
```
### Calculate Size of Array

```c
int main() {    // main function

    int numbers[] = {10,20,30,40,50};   // array
    char grades[] = {'A','B','C','D','F'};

    int size = sizeof(numbers) / sizeof(numbers[0]);   // calculate # of elements
    
    for (int i = 0; i < size; i++) {   // for loop to print all elements
        printf("%d ", numbers[i]);
    }

    return 0;

}
```