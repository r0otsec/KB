---
tags:
  - programming
  - C
date: 2025-08-07
---
# Read Files

- Files can be opened easily.
- Built in `struct` called FILE provided by `<stdio.h>`.
- Data type is `FILE`.
- Typically need a buffer:
	- waiting room/stores data temporarily to read such as a character array
## Syntax

- `fopen()` - attempts to open a file providing a path and mode (`r`)
	- e.g. `fopen("input.txt", "r")`
- If unable to create/open a file, it will return `NULL`
- Buffer declared using char array (typically 1024 bytes):
	- `char buffer[1024] = {0}`
- Can use while loop w/ `fgets`to read contents:
	- `while (fgets() != NULL)`
- Fgets requires things:
	- buffer (where text is stored)
	- size of buffer (`sizeof`)
	- pointer to file
	- e.g. `while(fgets(buffer, sizeof(buffer), pFile) != NULL)`
## Code Block

## Read File

```c
int main() {

    FILE *pFile = fopen("input.txt", "r");  // open file
    char buffer[1024] = {0};   // allocated buffer, initialize w/ 0

    if (pFile == NULL) {
        printf("Could not open file!");
        return 1;
    }

    while(fgets(buffer, sizeof(buffer), pFile) != NULL) {  // read file contents
        printf("%s", buffer);
    }

    fclose(pFile);

    return 0;

}
```