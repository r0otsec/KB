# Nested Loops

- Loops inside loops
- Combination of while, do or for loops
## Syntax

- Nested for loops should change variable name from `i` to `j` (best practice):
	- e.g. `for (int j = 1; i < 10; i++)`
## Code Blocks

### Repeated For Loops

```c
int main() {    // main function

    for (int i = 1; i < 10; i++) {   // define for loop count to 10
        printf("%d ", i);
    }
    printf("\n");

    for (int i = 1; i < 10; i++) {   // define for loop count to 10
        printf("%d ", i);
    }
    printf("\n");

    for (int i = 1; i < 10; i++) {   // define for loop count to 10
        printf("%d ", i);
    }
    printf("\n");

    return 0;

}
```
### Nested For Loops

```c
int main() {    // main function

    for (int i = 1; i < 4; i++) {
        for (int j = 1; j < 10; j++) {   // define for loop count to 10
            printf("%d ", j);
        }
        printf("\n");
    }

    return 0;

}
```
### Multiplication Table

```c
int main() {    // main function

    // Multiplication table creation
    for (int i = 1; i <= 10; i++) {
        for (int j = 1; j <= 10; j++) {
            printf("%3d ", i * j);
        }
        printf("\n");     
    }    

}
```