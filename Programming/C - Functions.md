---
tags:
  - programming
  - C
date: 2025-08-07
---
# Functions

>[!quote] Repetition
>In coding, don't repeat yourself!

- Reusable section of code.
- Can be invoked (called).
- Arguments can be sent to be used within function.
## Syntax

- Starts with [[C - Return|return type]]:
	- e.g. `void` (no return type)
- Includes the name of the function:
	- e.g. `void function () {`
- Functions should include any code to be reused.
- Functions must be called via the function name and brackets:
	- e.g. `function()`

>[!important] Arguments vs Parameters
>Arguments are what you send a function. Parameters are what the function expects to receive.
## Arguments

- Functions can't see in other functions (e.g. `function()` --> `main()`).
- Pass variables/values as arguments inside brackets with variable names:
	- e.g. `function(name, age)`
- Must also setup the function declaration with data type of receiving data and name of received data:
	- e.g. `void function(char name[], int age)`
- Arguments and parameters do not have to be the same name, but must match the type execpted.
## Code Blocks

### Basic Function

```c
void happyBirthday() {   // function declaration (void type)

    printf("\nHappy birthday to you!");
    printf("\nHappy birthday to you!");
    printf("\nHappy birthday dear [name]!");
    printf("\nHappy birthday to you!");
    printf("\nYou are [age] years old!\n");

}

int main() {    // main function
 
    happyBirthday();   // invoking function
	happyBirthday();
	happyBirthday();

    return 0;

}
```
### Arguments

```c
void happyBirthday(char name[], int age) {   // declaration w/ parameters

    printf("\nHappy birthday to you!");
    printf("\nHappy birthday to you!");
    printf("\nHappy birthday dear %s!", name);
    printf("\nHappy birthday to you!");
    printf("\nYou are %d years old!\n", age);

}

int main() {    // main function

    char name[] = "Jonny";
    int age = 29;

    happyBirthday(name, age);   // invoking function w/ args

    return 0;

}
```
### User Input

```c
void happyBirthday(char name[], int age) {   // function declaration (void type)

    printf("\nHappy birthday to you!");
    printf("\nHappy birthday to you!");
    printf("\nHappy birthday dear %s!", name);
    printf("\nHappy birthday to you!");
    printf("\nYou are %d years old!\n", age);

}

int main() {    // main function

    char name[50] = "";
    int age = 0;

    printf("Please enter your name: ");
    fgets(name, sizeof(name), stdin);   // receive user input (string)
    name[strlen(name) - 1] = '\0';  // remove newline char

    printf("Enter your age: ");
    scanf("%d", &age);    // receive user input (number)

    happyBirthday(name, age);   // invoking function w/ args

    return 0;

}
```