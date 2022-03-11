# 1 C Programming: Loading large text files into memory

Load a large text file into memory
	- Don't know size ahead of time
	- Conserve RAM (don't waste space)
	- Dynamically sized
	- Each like a separate string
	- Random access to each string


(An array to manage the first character element of each string->chars)
=>
char \* stringLinkArray[n]
[char \*](0) -> [chars](string)
[char \*](1) -> [chars](string)
[char \*](2) -> [chars](string)
[char \*](3) -> [chars](string)
...
[char \*](n) -> [chars](string)

***Techniques to dynamically assign the length of each string***
- Use a string buffer with long enough length for reading the string from file.
- Calculate the length of the temp string
- Assign the length for each [char](string)

char \*\* -> stringLinkArray[0]

23`28`

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char **loadfile(char *filename, int *len);

int main(int argc, char *argv[]) 
{
    if (argc == 1)
    {
        fprintf(stderr, "Must supply a filename to read\n");
        exit(1);
    }

    // Load file into data structure
    int length = 0;
    char **words = loadfile(argv[1], &length);

    // Display the first 100 lines

    return 0;
}

char **loadfile(char *filename, int *len)
{
    FILE *f = fopen(filename, "r");
    if (!f)
    {
        fprintf(stderr, "Can't open %s for reading\n", filename);
        return NULL;
    }

    // Allocate space for 100 char *
    char **lines = (char **)malloc(100 * sizeof(char *));
    char buf[1000];
    int i = 0;
    while (fgets(buf, 1000, f))
    {
        if (i == 100)
        {
            realloc(lines, 200 * sizeof(char *));
        }

        // Trim off newline char
        buf[strlen(buf)] = '\0';

        // Get length of buf
        int slen = strlen(buf);

        // Allocate space for the string
        char *str = (char *)malloc((slen + 1) * sizeof(char));

        // Copy string from buf to str
        strcpy(str, buf);

        // Attach str to data structure
        lines[i] = str;

        i++;
    }
}
```