---
tags:
  - programming
  - C
date: 2025-08-07
---
# Structs

- Custom containers
- Holds multiple pieces of related info.
- Similar to objects.
- Like a blueprint
## Syntax

- Declared outside of main function
- Defined as `struct [TagName] {};`
- Define items within the curly brackets (members)
	- all students have name, age, etc...
- Use within main function via `struct [TagName] [varName]`
- Can use `typedef` before struct keyword too.
- Member access operator is `.`:
	- e.g. `student1.name`
- Declare struct without values - `Student student4;`
	- returns undefined behaviour (random memory values)
- Assign values later via`strcpy()`:
	- `#include <string.h>`
	- `strcpy(student4.name, "Sandy")`
## Code Block

### Struct Definition

```c
struct Student{
    char name[50];
    int age;
    float gpa;
    bool isFullTime;
};
```
### Struct Typedef

```c
typedef struct{
    char name[50];
    int age;
    float gpa;
    bool isFullTime;
}Student;

int main() {    // main function

    Student student1 = {"Spongebob", 30, 3.2, true};

    return 0;

}
```
### Struct w/ Ternary

```c
typedef struct{
    char name[50];
    int age;
    float gpa;
    bool isFullTime;
}Student;

int main() {    // main function

    Student student1 = {"Spongebob", 30, 3.2, true};

    printf("%s\n", student1.name);  // grab name from struct
    printf("%d\n", student1.age);   // grab age from struct
    printf("%.1f\n", student1.gpa);  // grab gpa from struct
    printf("%s\n", (student1.isFullTime) ? "Yes" : "No");  // grab bool (ternary)
    return 0;

}
```
### Strncpy

```c
typedef struct{
    char name[50];
    int age;
    float gpa;
    bool isFullTime;
}Student;

int main() {    // main function

    Student student1 = {"Spongebob", 30, 3.2, true};
    Student student2 = {"Patrick", 36, 1.2, false};
    Student student3 = {"Squidward", 42, 3.9, false};
    Student student4 = {0};

    strncpy(student4.name, "Sandy", 5);

    printf("%s\n", student4.name);  // grab name from struct
    printf("%d\n", student4.age);   // grab age from struct
    printf("%.1f\n", student4.gpa);  // grab gpa from struct

    printf("%s\n", (student1.isFullTime) ? "Yes" : "No");  // grab bool (ternary)
    return 0;

}
```
### Pass Struct to Function

```c
typedef struct{
    char name[50];
    int age;
    float gpa;
    bool isFullTime;
}Student;

void printStudent(Student student);

int main() {    // main function

    Student student1 = {"Spongebob", 30, 3.2, true};
    Student student2 = {"Patrick", 36, 1.2, false};
    Student student3 = {"Squidward", 42, 3.9, false};
    Student student4 = {0};

    strncpy(student4.name, "Sandy", 5);
    student4.age = 27;
    student4.gpa = 4.0;
    student4.isFullTime = true;

    printStudent(student1);
    
    return 0;

}

void printStudent(Student student) {
 
    printf("%s\n", student.name);  // grab name from struct
    printf("%d\n", student.age);   // grab age from struct
    printf("%.1f\n", student.gpa);  // grab gpa from struct
    printf("\n");
    
}
```