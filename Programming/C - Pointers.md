---
tags:
  - programming
  - C
date: 2025-08-07
---
# Pointers

- Variable storing memory address of another variable.
- Avoids wasting memory.
- Allows passing address of a large data structure instead of copying entire data.

![[pointers.jpg]]
## Syntax

- `%p` - format specifier for pointers
- `&` - returns memory address of a variable (addressof operator)
	- e.g. `printf("%p", &age)`
- `*` - creates pointer (dereference operator `*`)
- `p[varName]` - standard naming convention for pointers:
	- e.g. `int *pAge = &age;`
## Understanding

- Returned mem address (`000000BF579FF8AC`) can be stored as a value in another var.
- Can pass pointer to various functions.
- Functions in C are **pass by value**:
	- passed values are copied (increment does not change original).
- To change variable within another function, use **pass by reference** via passing a pointer:
	- `e.g. pAge`
- If passing a pointer, parameter must accept a pointer by adding `*`.

Following code is an example:

```c
void birthday(int* age);

int main() {

    int age = 25;  // stores 25 (has mem addr)
    int *pAge = &age;  // declares pointer, stores address of age var

    birthday(pAge);

    printf("You are %d years old", age);
    return 0;

}

void birthday(int* age) {   // accepts pointer to integer
    age++;
}
```

- Parameter was set to age.
- The address of `age` was incremented, not the value.
	- must dereference via dereference operator
		- returns value at a given address (`*`)

Fixed code example:

```c
void birthday(int* age);

int main() {

    int age = 25;  // stores 25 (has mem addr)
    int *pAge = &age;  // declares pointer, stores address of age var

    birthday(pAge);

    printf("You are %d years old", age);
    return 0;

}

void birthday(int* age) {   // accepts pointer to integer
    (*age)++;
}
```
## Increment Understanding

- The code `void birthday(int* age)` means:
	- **age** is a **pointer to an int** - holding memory address of age from main()
- This means `age` is a **pointer to an int** — it’s holding the memory address of the `age` variable from `main()`.
- The code `(*age)++;` means:

> “Go to the memory address stored in `age` (i.e. `0x1234`), **dereference it** to access the actual value stored there, and **increment it by 1**.”

So:
- `*age` → gives you the value **at** address `0x1234`, which is `25`
- `(*age)++` → increments that value **in memory** → now it’s `26`
## Video Explanation

<div class="video-container"><iframe width="560" height="315" src="https://www.youtube.com/embed/2ybLD6_2gKM?si=FwCGx4Xc-ODdIWJF" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></div>

## Code Blocks

### Pointer Variable

```c
int main() {

    int age = 25;  // stores 25 (has mem addr)
    int *pAge = &age;  // declares pointer, stores address of age var

    printf("%p\n", &age);  
    printf("%p", pAge);    // both return the same
    return 0;

}
```
### Pass by Reference 

```c
void birthday(int* age);

int main() {

    int age = 25;  // stores 25 (has mem addr)
    int *pAge = &age;  // declares pointer, stores address of age var

    birthday(pAge);

    printf("You are %d years old", age);
    return 0;

}

void birthday(int* age) {   // accepts pointer to integer
    (*age)++;  // Go to that address, grab the value, increment
}
```