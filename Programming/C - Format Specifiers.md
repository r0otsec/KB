---
tags:
  - programming
  - C
date: 2025-08-07
---
# Format Specifiers

- Special tokens to specify data type/optional modifiers
- Control how data is displayed/interpreted
## Specifiers

- `%d` - format specifier for integer
- `%f` - format specifier for floats
	- `%.1f` - specifies number of digits for floats (e.g. 1)
- `%lf` - format specifier for long float
	- `%.15lf` - specifies number of digits for doubles (e.g. 15)
- `%c` - format specifier for character
- `%s` - format specifier for string/array of characters
## Modifiers

- `%3d` - specifies width (empty spaces on left)
- `%-3d` - specifies width (empty spaces on right)
- `%03d` - specifies leading zeroes
- `%+d` - adds symbol before (+ or -)
- `%.2f` - specifies number of digits for floats
## Code Blocks

### Specifiers

```c
int main() {      // main function - required!

    int age = 25;
    float price = 19.99;
    double pi = 3.1415926535;
    char currency = '$';
    char name[] = "THOR";

    printf("Age: %d\n", age);   // print integer
    printf("Price: %f\n", price);   // print float
    printf("Pi: %lf\n", pi);   // print double
    printf("Currency: %c\n", currency);   // print single char
    printf("Name: %s\n", name);   // print string

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Positives/Negatives

```c
int main() {      // main function - required!

    int num1 = 1;
    int num2 = 10;
    int num3 = -100;

    printf("%+d\n", num1);
    printf("%+d\n", num2);
    printf("%+d\n", num3);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```
### Floats

```c
int main() {      // main function - required!

    float price1 = 19.99;
    float price2 = 1.50;
    float price3 = -100.00;

    printf("%.2f\n", price1);
    printf("%.2f\n", price2);
    printf("%.2f\n", price3);

    return 0;     // main func expected to return int, exit code (0 = good)

}
```