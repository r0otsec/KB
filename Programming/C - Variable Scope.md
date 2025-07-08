# Variable Scope

- Scope = where a variable is recognized/accessible.
- Variables can share names if in different scopes.
- Anything within `{}` is a local scope.
## Global Scope

- Defines variables outside functions.
- Can be used anywhere else.
- Not recommended:
	- hard to debug as any function could modify it unintentionally
- Only recommended for constants.
## Code Blocks

### Working Example

```c
int add(int x, int y) {

    int result = x + y;   // result variable under add()
    return result;

}

int main() {    // main function

    int result = add(3, 4);   // // result variable under main()
    printf("%d", result);

}
```
### Broken Example (Not Declared)

```c
int add(int x, int y) {

    int result = x + y;   // result variable under add()
    return result;

}

int subtract() {

    int result = x - y;
    return result;

}

int main() {    // main function

    int x = 5;
    int y = 6;

    int result = subtract();

    printf("%d", result);

}
```
### Global Scope

```c
int result = 0;    // Global Scope

int add(int x, int y) {

    result = x + y;   // result variable under add()
    return result;

}

int subtract(int x, int y) {

    result = x - y;
    return result;

}

int main() {    // main function

    int x = 5;
    int y = 6;

    result = subtract(x,y);

    printf("%d", result);

}
```