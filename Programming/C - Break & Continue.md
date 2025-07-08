---
tags:
  - programming
  - C
date: 2025-08-07
---
# Break & Continue

- `break` - break out of a loop (stop)
- `continue` - skip current cycle of a loop (skip)
## Code Blocks

### Break

```c
int main() {    // main function

    for (int i = 1; i <= 10; i++) {
        
        if (i == 4) {   // if i is 4
            break;    // exit loop
        }

        printf("%d\n", i);

    }

    return 0;

}
```
### Continue

```c
int main() {    // main function

    for (int i = 1; i <= 10; i++) {
        
        if (i == 4) {   // if i is 4
            continue;    // skip and move to 5
        }

        printf("%d\n", i);

    }

    return 0;

}
```