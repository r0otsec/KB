# Return

- `return` simply returns a value back to where you call a function.
- Function can send something back when called.
## Return Types

- Precede name of functions (`[type] function()`)
	- e.g. `int main()`
- `return` keyword returns value/variable to where function was called:
	- e.g. `return result`
- If returning value/variable, must list data type of what is returning in function declaration:
	- e.g. `int square()`
## Main Function

- Main function returns 0 as an integer (`int main()`, `return 0`).
- 0 serves as exit code
- If returning a number >0, it means an error
## Code Blocks

### Square Function

```c
int square(int num) {

    int result = num * num;
    return result;

	// can be simplified to return num * num
}

int main() {    // main function

    int x = square(2);   // functino call replaced with value 4
    int y = square(3);   // function call replaced with value 9
    int z = square(4);   // function call replaced with value 16

    printf("%d\n", x);
    printf("%d\n", y);
    printf("%d\n", z);

    return 0;

}
```
### Double Function

```c
double square(double num) {

    return num * num;

}

int main() {    // main function

    double x = square(2.1);
    double y = square(3.2);
    double z = square(4.3);

    printf("%lf\n", x);
    printf("%lf\n", y);
    printf("%lf\n", z);

    return 0;

}
```
### Boolean Function

```c
bool ageCheck(int age) {

    if (age >= 18) {
        return true;
    }
    else {
        return false;
    }

}

int main() {    // main function

    int age = 12;

    if (ageCheck(age)) {
        printf("You may sign up");
    }
    else {
        printf("You must be 18+ to sign up");
    }

    return 0;

}
```
### Get Max Number

```c
int getMax(int x, int y) {

    if (x >= y) {
        return x;
    }
    else {
        return y;
    }

}

int main() {    // main function

    int max = getMax(4, 5);
    printf("%d", max);

    return 0;

}
```