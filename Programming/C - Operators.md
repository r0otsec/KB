---
tags:
  - programming
  - C
date: 2025-08-07
---
# Operators

- Various arithmetic operators available.
# Arithmetic Operations

- `equals (=)`
- `+ (plus)` - adds numbers
- `- (minus)` - subtracts numbers
- `* (multiply)` - multiplies numbers
- `/ (divide)` - divides numbers
	- decimals do not store decimal portions
	- must change numbers to float if result not integer
- `% (modulo)` - shows remainder
- `++ (increment)` - increment by value
- `-- (decrement)` - decrement by value
- `comparison (==)` - comparison operator
## Augmented Assignment Operators

- `x += 2` - Apply if reassigning the same variable
	- same as `x = x + 2`
## Code Blocks

### Addition

```c
int main() {      // main function - required!

    int x = 2;
    int y = 3;
    int z = 0;

    z = x + y;
    printf("%d", z);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Subtraction

```c
int main() {      // main function - required!

    int x = 2;
    int y = 3;
    int z = 0;

    z = x - y;
    printf("%d", z);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Multiplication

```c
int main() {      // main function - required!

    int x = 2;
    int y = 3;
    int z = 0;

    z = x * y;
    printf("%d", z);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Division

```c
int main() {      // main function - required!

    int x = 2;
    float y = 3;
    float z = 0;

    z = x / y;
    printf("%f", z);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Modulo

```c
int main() {      // main function - required!

    int x = 10;
    int y = 3;
    int z = 0;

    z = x % y;
    printf("%d", z);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Increment

```c
int main() {      // main function - required!

    int x = 10;
    int y = 3;
    int z = 0;

    x++;
    printf("%d", x);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Decrement

```c
int main() {      // main function - required!

    int x = 10;
    int y = 3;
    int z = 0;

    x--;
    printf("%d", x);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Augmented Assignment

```c
int main() {      // main function - required!

    int x = 10;
    int y = 3;
    int z = 0;

    x+=2;
    printf("%d", x);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```