# Function Prototypes

- Listed before main function
- Provides info about:
	- function name
	- return type
	- parameters
- Enables type checking.
- Allows functions to be used before defined.
- Improves readability, organization and errors.
## Syntax

- Example syntax - `void hello(char name[], int age);`.
- Should contain code within.
## Function Issues

- C programs read top to bottom.
- Functions must be defined before being invoked/called.
- Main function always at the bottom.
- Prototypes allow the main function to be first by declaring the prototype;
## Code Blocks

### Prototype Declaration

```c
void hello(char name[], int age) {

    printf("Hello %s\n", name);
    printf("You are %d years old\n", age);
}

int main() {    // main function

    hello("Jonny", 29);
    return 0;

}
```
### Prototype First

```c
void hello(char name[], int age);    // function prototype

int main() {    // main function

    hello("Jonny", 29);
    return 0;

}

void hello(char name[], int age) {

    printf("Hello %s\n", name);
    printf("You are %d years old\n", age);
}
```