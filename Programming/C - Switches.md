# Switches

- Alternative to many if-else-statements
- More efficient w/ fixed integer values and char values
- Easier to read (don't be YandereDev!)

## Syntax

- `switch (value) {` - start a switch statement & examine value
- `case 1:` - first case (i.e. value == 1)
- `break` - break out of the switch
	- if not declared, that case is printed and cascade until next break statement
- `default:` - default case if no matches
## Code Blocks

### Simple Switch

```c
int main() {

    int dayOfWeek = 0;

    switch (dayOfWeek) {
        case 1:
            printf("It is Monday");
            break;
        case 2:
            printf("It is Tuesday");
            break;
        case 3:
            printf("It is Wednesday");
            break;
        case 4:
            printf("It is Thursday");
            break;
        case 5:
            printf("It is Friday");
            break;
        case 6:
            printf("It is Saturday");
            break;
        case 7:
            printf("It is Sunday");
            break;
    }

    return 0;

}
```
### Default Case

```c
int main() {

    int dayOfWeek = 12;

    printf("Enter day of the week (1 -> 7): ");
    scanf("%d", &dayOfWeek);

    switch (dayOfWeek) {
        case 1:
            printf("It is Monday");
            break;
        case 2:
            printf("It is Tuesday");
            break;
        case 3:
            printf("It is Wednesday");
            break;
        case 4:
            printf("It is Thursday");
            break;
        case 5:
            printf("It is Friday");
            break;
        case 6:
            printf("It is Saturday");
            break;
        case 7:
            printf("It is Sunday");
            break;
        default:
            printf("Please enter a number 1 through 7");   // default case
    }

    return 0;

}
```
### Character Switch

```c
int main() {

    char dayOfWeek = '\0';  // initialize char

    printf("Enter day of the week (M, T, W, R, F, S, U): ");
    scanf("%c", &dayOfWeek);

    switch (dayOfWeek) {
        case 'M':
            printf("It is Monday");
            break;
        case 'T':
            printf("It is Tuesday");
            break;
        case 'W':
            printf("It is Wednesday");
            break;
        case 'R':
            printf("It is Thursday");
            break;
        case 'F':
            printf("It is Friday");
            break;
        case 'S':
            printf("It is Saturday");
            break;
        case 'U':
            printf("It is Sunday");
            break;
        default:
            printf("Please enter a character (M, T, W, R, F, S, U)");   // default case
    }

    return 0;

}
```