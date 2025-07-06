# User Input

- If assigning an empty variable like a char array, the blocks of memory the variables are using may already contain values from previous use.
	- Can lead to undefined behaviour.
- Best practice to assign dummy values to variables

```c
int age = 0;          // declare unassigned variable
float gpa = 0.0f;     // "f" shows it should be a float
char grade = '\0';    // null terminator (clear it out if a char)
char name[30] = "";        // max size of 30 chars, can be empty string (still 30)
```
## Input

- `scanf` - gets user input
	- `&age` - "address of" operator (at address, store value)
- ` %c` - add space before specifier to clear input buffer to avoid issues
- `fgets` - file get string (better for full names and whitespace issues)
	- syntax is `fgets(var_name, sizeof(var_name), stdin);`
	- issue - accepts enter as part of input (inc. new line)
- `getchar()` - clears new line in input buffer
- `#include <string.h>` - provides useful functions for strings
- `strlen()` - function to grab length of provided string/variable
- `var_name[strlen(var_name) - 1] = '\0';`
	- sample code to remove new line from fgets
## Code Blocks
### Integer Input

```c
int main() {      // main function - required!

    int age = 0;          // declare unassigned variable

    printf("Enter an age: ");

    scanf("%d", &age); 
    printf("%d\n", age);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Float Input

```c
int main() {      // main function - required!

    float gpa = 0.0f;

    printf("Enter your GPA: ");
    scanf("%f", &gpa);

    printf("%.2f\n", gpa);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Char Input

```c
int main() {      // main function - required!

    char grade = '\0';

    printf("Enter your grade: ");
    scanf("%c", &grade);

    printf("%c\n", grade);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Input Buffer Issue

```c
int main() {      // main function - required!

    int age = 0;          // declare unassigned variable
    float gpa = 0.0f;     // "f" shows it should be a float
    char grade = '\0';    // null terminator (clear it out if a char)
    char name[30] = "";        // max size of 30 chars, can be empty string (still 30)

    printf("Enter an age: ");
    scanf("%d", &age); 

    printf("Enter your GPA: ");
    scanf("%f", &gpa);

    printf("Enter your grade: ");
    scanf(" %c", &grade);   // space added to clear buffer

    printf("%d\n", age);
    printf("%.1f\n", gpa);
    printf("%c\n", grade);
    printf("%c\n", name);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Fgets Function

```c
int main() {      // main function - required!

    int age = 0;          // declare unassigned variable
    float gpa = 0.0f;     // "f" shows it should be a float
    char grade = '\0';    // null terminator (clear it out if a char)
    char name[30] = "";        // max size of 30 chars, can be empty string (still 30)

    printf("Enter an age: ");
    scanf("%d", &age); 

    printf("Enter your GPA: ");
    scanf("%f", &gpa);

    printf("Enter your grade: ");
    scanf(" %c", &grade);

    getchar();        // clears input buffer
    printf("Enter full name: ");
    fgets(name, sizeof(name), stdin);    // alt to scanf (handles whitespace)

    printf("%d\n", age);
    printf("%.1f\n", gpa);
    printf("%c\n", grade);
    printf("%s\n", name);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Strings Header Function

```c
int main() {      // main function - required!

    int age = 0;          // declare unassigned variable
    float gpa = 0.0f;     // "f" shows it should be a float
    char grade = '\0';    // null terminator (clear it out if a char)
    char name[30] = "";        // max size of 30 chars, can be empty string (still 30)

    printf("Enter an age: ");
    scanf("%d", &age); 

    printf("Enter your GPA: ");
    scanf("%f", &gpa);

    printf("Enter your grade: ");
    scanf(" %c", &grade);

    getchar();        // clears input buffer
    printf("Enter full name: ");
    fgets(name, sizeof(name), stdin);    // alt to scanf (handles whitespace)
    name[strlen(name) - 1] = '\0';

    printf("%s\n", name);
    printf("%d\n", age);
    printf("%.1f\n", gpa);
    printf("%c\n", grade);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```