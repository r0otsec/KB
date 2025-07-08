---
tags:
  - programming
  - C
date: 2025-08-07
---
# While Loops

- Continues code WHILE condition remains true.
- Condition must be true to enter the loop.
- Great for accepting user input:
	- if not valid input, prompt them again for example.
## Syntax

- `while()` - define a while loop
	- brackets should contain a condition.
	- try avoiding infinite loops (e.g. `1 == 1`);
## Do While Loop

- Runs code once first.
- Checks condition at the end
## Do While Syntax

- `do` - starts do while loop
- `while()` - defined after the `do` section.
## Code Blocks

### Basic While Loop

```c
int main() {    // main function

    int num = 0;

    while(num <= 0) {
        printf("Enter a number greater than 0: ");
        scanf("%d", &num);
    }

}
```
### Do While

```c
int main() {    // main function

    int num = 1;

    do {
        printf("Enter a number greater than 0: ");
        scanf("%d", &num);
    } while(num <= 0);    // check condition at end

    return 0;

}
```
### Example - String

```c
int main() {    // main function

    char name[50] = "";

    printf("Enter your name: ");
    fgets(name, sizeof(name), stdin);  // accept user input
    name[strlen(name) - 1] = '\0';   // remove new line

    while(strlen(name) == 0) {
        printf("Name cannot be empty! Enter your name: ");
        fgets(name, sizeof(name), stdin);
        name[strlen(name) - 1] = '\0';
    }

    printf("Hello %s", name);

    return 0;

}
```
### Example - Boolean

```c
int main() {    // main function

    bool isRunning = true;
    char response = '\0';

    while(isRunning) {   // while true
        printf("You are playing a game\n");
        printf("Would you like to continue?: \n");
        scanf(" %c", &response);

        if (response != 'Y') {
        isRunning = false;
        }
    }

    printf("Thank you for playing!");

    return 0;

}
```