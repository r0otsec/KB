---
tags:
  - programming
  - C
date: 2025-08-07
---
# Math Functions

- Functions need the `<math.h>` header file.
# Functions

- `sqrt(x)` - calculates the square root of x
- `pow(x, 2)` - calculates power of number specified (i.e. 2)
- `round(x)` - rounds a float
	- `ceil(x)` - rounds up
	- `floor(x)` - rounds down
- `abs(x)` - absolute value (distance from 0)
- `log(x)` - calculates natural log
- `sin(x)` - calculates the sin
- `cos(x)` - calculates the cosin
- `tan(x)` - calculates the tangent
## Code Blocks

### Square Root

```c
#include <stdio.h>
#include <math.h>

int main() {

    int x = 9;

    x = sqrt(x);
    printf("%d", x);

    return 0;

}
```
### Power

```c
int main() {

    int x = 2;

    x = pow(x, 2);
    printf("%d", x);

    return 0;

}
```
### Round

```c
#include <stdio.h>
#include <math.h>

int main() {

    float x = 3.14;

    x = round(x);
    printf("%f", x);

    return 0;

}
```
### Ceiling

```c
int main() {

    float x = 3.14;

    x = ceil(x);
    printf("%f", x);

    return 0;

}
```
### Floor

```c
int main() {

    float x = 3.99;

    x = floor(x);
    printf("%f", x);

    return 0;

}
```
### Absolute

```c
int main() {

    int x = -3;

    x = abs(x);
    printf("%d", x);

    return 0;

}
```
### Log

```c
int main() {

    float x = 3;

    x = log(x);
    printf("%f", x);

    return 0;

}
```
### Sin

```c
int main() {

    float x = 45;

    x = sin(x);
    printf("%f", x);

    return 0;

}
```
### Cosin

```c
int main() {

    float x = 45;

    x = cos(x);
    printf("%f", x);

    return 0;

}
```
### Tangent

```c
int main() {

    float x = 45;

    x = tan(x);
    printf("%f", x);

    return 0;

}
```