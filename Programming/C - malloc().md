---
tags:
  - programming
  - C
date: 2025-08-07
---
# malloc()

- Function to dynamically allocate a specific number of bytes in memory.
- Solves fixed-size array problems (e.g. `char grades[5]`)
## Syntax

- Requires `#include <stdlib.h>`
- If # of elements is unknown, return a pointer from `malloc()`
- Create pointer to array-like data structure, returned by malloc():
	- e.g. `char *grades = malloc(100);`
- `malloc()` requires bytes to reserve in memory:
	- e.g. `malloc(100)`
- Can dynamically generate bytes by asking user:
	- e.g. ``
- Can free up memory space via `free()` function:
	- e.g. `free(grades)` returns rented space to OS.

## Understanding

- `char` is typically 1 byte
- `int` is typically 4 bytes
- Can calculate size needed instead of hardcoding.
- Memory reserve need is from a location called the `heap`.
	- most situations when using memory takes it from the `stack`.
- `char *grades = malloc(number * sizeof(char))` as an example:
	- returns pointer to where reserved memory is located.
- Very important to return the space/free up the memory via `free()`
	- also must reset the pointer by setting it to NULL (e.g. `grades = NULL`)
		- avoids **dangling pointers**
- Pointers unlock a value at a memory address when de-referenced.
## Further Understanding

- If `char *grades = malloc(number * sizeof(char))` fails, it returns NULL.
	- important to check as dereference NULL pointers can cause segmentation faults.
- Arrays could use `sizeof()` for for loops
	- does not work here
	- `*grades` is a pointer to an array-like data structure
	- would grab size of pointer
- Solved by taking user input (e.g. `i < number`)
## Code Blocks

## Malloc() Example

```c
int main() {

    int number = 0;
    printf("Enter number of grades: ");
    scanf("%d", &number);

    char *grades = malloc(number * sizeof(char));

    if (grades == NULL) {   // checking for failed memory allocation
        printf("Memory allocation failed!\n");
        return 1;
    }    

    for (int i = 0; i < number; i++) {
        printf("Enter grade #%d: ", i + 1);  // offset to start at 1
        scanf(" %c", &grades[i]);   // can treat it like array (e.g. index)
    }

    for (int i = 0; i < number; i++) {
        printf("%c ", grades[i]);
    }

    free(grades);   // returns rented space to OS
    grades = NULL;  // avoids dangling pointers

    return 0;

}
```