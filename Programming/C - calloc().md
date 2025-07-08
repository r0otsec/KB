---
tags:
  - programming
  - C
date: 2025-08-07
---
# calloc()

- (C)ontinuous (alloc)ation.
- Allocates memory dynamically.
- Sets all allocated bytes to 0.
- calloc()
	- sets all allocated bytes to 0 (clear)
	- requires 2 arguments (`calloc(#, size)`:
		- number of elements
		- size of each element
- malloc()
	- pass in number of bytes (`malloc(bytes)`)

## Syntax

- Requires `#include <stdlib.h>`
- Requires two arguments - **number** and **size**
	- e.g. `calloc(number, sizeof(int))`
		- sets 10 numbers (40 bytes) to 0
## Code Blocks

### Calloc Example

```c
int main() {

    int number = 0;
    printf("Enter the number of players: ");
    scanf("%d", &number);

    int *scores = calloc(number, sizeof(int)); // calloc resets to 0

    // check to see if pointer == NULL
    if (scores == NULL) {
        printf("Memory allocation failed!");
        return 1;
    }

    for (int i = 0; i < number; i++) {
        printf("Enter score #%d: ", i + 1);   // Ask user for score 1
        scanf("%d", &scores[i]);
    }

    // cycle through array-like data struct
    for (int i = 0; i < number; i++) {
        printf("%d ", scores[i]);   // prints the scores
    }

    free(scores);   // frees up memory
    scores = NULL;  // set pointer to NULL once done

    return 0;

}
```