---
tags:
  - programming
  - C
date: 2025-08-07
---
# Typedef

- Reserved keyword
- Provides existing datatype a "nickname"
- Helps simplify complex types/readability.
- Could rename char arrays to normal strings.
## Syntax

- `typedef existing_type new_name` - format
	- e.g. `typedef int Number`
- New nickname can be used (e.g. Number) instead of int.
- Create a string type by renaming char:
	- `typedef char String[NUM]`
		- NUM = specify size (char limit)
## Code Blocks

### Int Renamed

```c
typedef int Number;

int main() {    // main function

    Number x = 3;
    Number y = 4;
    Number z = x + y;

    printf("%d", z);

    return 0;

}
```
### String

```c
typedef char String[50];

int main() {    // main function

    String name = "Jonny Pake";

    printf("%s", name);

    return 0;

}
```
### Initials

```c
typedef char String[50];
typedef char Initials[3];

int main() {    // main function

    Initials user1 = "JP";
    Initials user2 = "SS";
    Initials user3 = "PS";
    Initials user4 = "ST";

    printf("%s\n", user1);
    printf("%s\n", user2);
    printf("%s\n", user3);
    printf("%s\n", user4);

    return 0;

}
```