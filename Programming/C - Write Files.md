---
tags:
  - programming
  - C
date: 2025-08-07
---
# Write Files

- Files can be written to easily.
- Built in `struct` called FILE provided by `<stdio.h>`.
- Data type is `FILE`.
## Syntax

- `fopen()` - attempts to open a file providing a path and mode (`r`,`w`)
	- e.g. `fopen("C:\testfile.txt", "w")`
- Good practice to close the file when done via `fclose(pFile);`.
- IF unable to create/open a file, it will return `NULL`
- Write data to a file (e.g. char array/string) via `fprintf()` with 3 args:
	- `fprint(POINTER,SPECIFIER,TEXT)`
	- e.g. `fprint(pFile, "%s", text);`
## Code Blocks

### Basic File Open

```c
int main() {

    FILE *pFile = fopen("C:\\Users\\THOR\\output.txt", "w");   // open file to write

    if (pFile == NULL) {
        printf("Error opening file\n");
        return 1;  // end program prematurely, exit code
    }

    fclose(pFile);   // close file, free resources

    return 0;

}
```
### Write to File

```c
int main() {

    FILE *pFile = fopen("C:\\Users\\THOR\\output.txt", "w");   // open file to write

    char text[] = "NEW\nFILE\nCREATED";

    if (pFile == NULL) {
        printf("Error opening file\n");
        return 1;  // end program prematurely, exit code
    }

    fprintf(pFile, "%s", text);   // write text to file
    printf("File was written successfully!");
    fclose(pFile);   // close file, free resources

    return 0;

}
```