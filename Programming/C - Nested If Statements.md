# Nested If Statements

- If statements within if statements within if statements
## Code Blocks

### Incorrect Code (Not Nested)

```c
int main() {

    float price = 10.00;
    bool isStudent = true;  // 10% discount if student (true)
    bool isSenior = true;   // 20 discount if senior (true)

    // Student = $9
    // Senior = $8
    // Senior Student = $7

    if (isStudent) {
        printf("You get a student discount of 10%\n");
        price *= 0.9;   // augmented operator
    }

    if (isSenior) {
        printf("You get a senior discount of 20%\n");
        price *= 0.8;   // augmented operator
    }

    printf("The price of a ticket is: $%.2f\n", price);  // decimals to 2 places

    return 0;

}
```
### Correct Code (Nested)

```c
int main() {

    float price = 10.00;
    bool isStudent = true;  // 10% discount if student (true)
    bool isSenior = true;   // 20 discount if senior (true)

    // Student = $9
    // Senior = $8
    // Senior Student = $7

    if (isStudent) {   // if student, enter this
        if (isSenior) {   // if senior + student, enter this
            printf("You get a student discount of 10%\n");
            printf("You get a senior discount of 20%\n");
            price *= 0.7;   // augmented operator
        }
        else {  // if student, enter this
        printf("You get a student discount of 10%\n");
        price *= 0.9;
        }
    }
    else {
        if (isSenior) {   // if senior, enter this
            printf("You get a senior discount of 20%\n");
            price *= 0.8;
        }
    }

    printf("The price of a ticket is: $%.2f\n", price);  // decimals to 2 places
    return 0;

}
```