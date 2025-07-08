# If Statements

- Do some code if a condition is true
- If false, don't do it
- No limit on else if statements.
## Syntax

- `if (conditionA) {` - declare an if statement (start)
- `else {` - alternative condition if not true
- `else if (conditionB) {` - check a second condition
## Order of Operations

- If statements are read top down
	- if the third statement and first statement are true, the first gets executed.
## Condensed Statements

- For multiple statements, they may be condensed such as:
	- `else if ((A == 1 && B == 3) || (A == 2 && B == 1) || (A == 3 && B == 2))`
## Code Blocks

### Basic If Statement

```c
int main() {

    int age = 12;
    
    if (age >= 18) {
        printf("You are an adult!");
    }
    else {
        printf("You are a child.");
    }

    return 0;

}
```
### Else If

```c
int main() {

    int age = -12;
    
    if (age >= 18) {
        printf("You are an adult!");
    }
    else if (age < 0){
        printf("You have not been born yet");
    }
    else {
        printf("You are a child.");
    }

    return 0;

}
```
### Boolean Example

```c
int main() {

    bool isStudent = true;

    if (isStudent) {    // don't need == true
        printf("You are a student");
    }
    else {
        printf("You are not a student");
    }

    return 0;

}
```
### Comparison

```c
int main() {

    char name[50] = "";
    
    printf("Enter your name: ");
    fgets(name, sizeof(name), stdin);   // grab user input
    name[strlen(name) - 1] = '\0';    // remove new line 

    if(strlen(name) == 0){    // check if string is empty
       printf("You did not enter your name");
    }
    else{
        printf("Hello %s", name);
    }

    return 0;

}
```