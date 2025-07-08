# For Loops

- Repeats code for `x` amount of times.
- Three optional steps:
	- Initialization
	- Condition
	- Update
# Syntax

- `for()` - start a for loop
- Parentheses includes three optional steps.
- Common counter defined as `for(int i = 0)`
- Condition example may be `for(int i = 0, i < 10)`
- Common update may be `for(int i = 0, i < 10, i++)`
	- iterates counter by 1 after each cycle
	- can also be decrement `i--`
- Increment by other numbers via `i+=2`
- Sleep function used via `Sleep(milliseconds)`
### Code Blocks

### Basic For Loop

```c
int main() {    // main function

    for (int i = 0; i < 10; i++) {
        printf("%d\n", i);
    }

    return 0;

}
```
### Sleep Function

```c
int main() {    // main function

    for (int i = 10; i >= 0; i--) {
        Sleep(1000);
        printf("%d\n", i);
    }

    printf("Happy New Year!");

    return 0;

}
```