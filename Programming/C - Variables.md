---
tags:
  - programming
  - C
date: 2025-08-07
---
# Variables

- Reusable containers for a value
## Data Types

Can contain different data types:

- `Integer` (number)
- `Float` (decimals up to 6/7 digits)
- `Double` (decimals up to 15/16 digits)
- `Char` (single characters)
- `String` (uses an array of characters, not a "string" type)
- `Boolean` (either TRUE (1) / FALSE (0))
	- must include the header file `#include <stdbool.h>`
## Constants

- `const` - use before variable declaration to not allow changes by mistake
	- constants should always be uppercase (e.g. `const double PI`)
## Code Examples

### Integers

```c
int main() {      // main function - required!

    int age = 29;
    int year = 2025;
    int quantity = 1;

    printf("You are %d years old\n", age);
    printf("The year is %d\n", year);
    printf("The quantity specified is %d", quantity);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Floats

```c
int main() {      // main function - required!

    float grade = 2.5;
    float price = 19.99;
    float temp = 27.2;

    printf("Your grade is %.1f\n", grade);
    printf("The price is £%.2f\n", price);
    printf("The temperature outside is %.1fC\n", temp);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Doubles

```c
int main() {      // main function - required!

    double pi = 3.14159265358979;
    double e = 2.71828182484590;

    printf("The value of pi is %.15lf\n", pi);
    printf("The value of e is %.15lf\n", e);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Chars

```c
int main() {      // main function - required!

    char grade = 'A';
    char symbol = '!';
    char currency = '$';

    printf("Your grade is %c\n", grade);
    printf("Your symbol is %c\n", symbol);
    printf("Your currency is %c\n", currency);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Strings

```c
int main() {      // main function - required!

    char name[] = "THOR";
    char machine[] = "ASGARD";
    char site[] = "https://rootsec.me";

    printf("The username is %s\n", name);
    printf("The hostname is %s\n", machine);
    printf("My new site is %s\n", site);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```

### Booleans

```c
int main() {      // main function - required!

    bool isOnline = true;

    printf("%d", isOnline); // returns value 1 if true, 0 if false

    return 0;     // main func expected to return int, exit code (0 = good)

}
```

```c
int main() {      // main function - required!

    bool isOnline = true;

    if(isOnline) {
        printf("You are online");
    }
    else {
        printf("You are offline");
    }

    return 0;     // main func expected to return int, exit code (0 = good)

}
```