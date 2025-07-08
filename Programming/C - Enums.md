---
tags:
  - programming
  - C
date: 2025-08-07
---
# Enums

- User defined data type
- Consists of set of named integer constants
- Replaces numbers with readable names
## Syntax

- `enum` - create set of enums
- Tag name required (like a data type):
	- e.g. `enum Day`
- Constants should be declared inside (always uppercase).
- `enum [DATATYPE] [VAR_NAME]` - use the enum with a constant
	- e.g. `enum Day today = SUNDAY;`
- Constants can be set with a number (default starting 0)
- Can be combined with `typedef`
## Code Blocks

### Enum Declaration

```c
enum Day{
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
};
```
### Weekdays

```c
enum Day{   // enum declaration
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
};

int main() {    // main function

    enum Day today = SUNDAY;
    printf("%d", today);  // prints 0 (SUNDAY)

    return 0;

}
```
### Typedef/Enums

```c
typedef enum {
    SUNDAY = 1, MONDAY = 2, TUESDAY = 3, WEDNESDAY = 4, THURSDAY = 5, FRIDAY = 6, SATURDAY = 7
}Day;

int main() {    // main function

    Day today = SUNDAY;
    printf("%d", today);  // prints 0 (SUNDAY)

    return 0;

}
```
### Connection

```c
#include <stdio.h>

typedef enum {    // typedef/enum declaration
    SUCCESS, FAILURE, PENDING
}Status;

void connectStatus(Status status); // func prototype

int main() {    // main function

    Status status = PENDING;

    connectStatus(status);

    return 0;

}

void connectStatus(Status status) {

    switch(status) {
        case SUCCESS:
            printf("Connection was successful\n");
            break;
        case FAILURE:
            printf("Could not connect\n");
            break;
        case PENDING:
            printf("Connecting...\n");
            break;
    }

}
```