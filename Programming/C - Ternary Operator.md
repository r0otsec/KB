---
tags:
  - programming
  - C
date: 2025-08-07
---
## Ternary Operator

- Shorthand for if-else statements.
- Write condition then use operator
## Syntax

- `?` - ternary operator character
	- `(condition) ? value_if_true : value_if_false`
## Code Blocks

### Basic Ternary Operation

```c
int main() {    // main function

    int x = 5;
    int y = 6;
    int max = (x > y) ? x : y;  // ternary operator

    printf("%d", max);

    return 0;

}
```
### Basic Ternary Boolean

```c
int main() {    // main function

    bool isOnline = false;

    printf("%s", (isOnline) ? "online" : "offline");

    return 0;

}
```
### Odd/Even

```c
int main() {    // main function

    int number = 8;

    printf("%d is %s", number, (number % 2 == 0) ? "Even" : "Odd");

    return 0;

}
```
### Clock

```c
int main() {    // main function

    int hours = 14;
    int minutes = 3;

    printf("%02d:%02d %s", hours, minutes, (hours < 12) ? "AM" : "PM" );

    return 0;

}
```