# Random Numbers

- Pseudo-random numbers
	- appear random but calculated by formulate w/ seed value
	- generates predictable sequence of numbers
	- not TRULY random
## Syntax

- Requires two header files:
	- `#include <stdlib.h>`
	- `#include <time.h>`
- Call random function - `rand()`
	- result is always the same due to the predictable seed (either 1 or 0)
- Create seed value based on current time:
	- `srand()` - random seed
	- `time(NULL)` - grab current time
- Display max number with `srand` using const `RAND_MAX`
	- `printf("%d", RAND_MAX)`
## Code Blocks

### Basic Random Number

```c
int main() {    // main function

    printf("%d", rand());

    return 0;

}
```
### Based on Time

```c
int main() {    // main function

    srand(time(NULL));
    printf("%d", rand());

    return 0;

}
```
### Basic Pseudo-Random Numbers

```c
int main() {    // main function

    srand(time(NULL));
    int randomNum = (rand() % 2) + 1;  // remainder of time / 2 + 1

    printf("%d", randomNum);

    return 0;

}
```
### Range Pseudo-Random

```c
int main() {    // main function

    srand(time(NULL));

    int min = 50;
    int max = 100;

    int randomNum = (rand() % (max - min + 1)) + min;  // num between 50-100
    printf("%d", randomNum);

    return 0;

}
```