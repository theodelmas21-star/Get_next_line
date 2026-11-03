# get_next_line

> A C programming project at 42 School that implements a function to read line-by-line from a file descriptor.

## Overview

**get_next_line** is a core algorithmic project designed to teach memory management, buffer manipulation, and the usage of static variables in C. The goal is to create a function that returns a single line read from a file descriptor, whether from a standard file, standard input, or a network stream, until the end of the file is reached.

## Features

- **Line-by-Line Reading**: Returns one complete line ending with `\n` (if present) on each function call.
- **Buffer Flexibility**: Supports dynamic buffer sizes via the `BUFFER_SIZE` macro defined at compilation.
- **Static Memory Handling**: Preserves leftover unread bytes between consecutive function calls.
- **Multiple File Descriptor Support (Bonus)**: Capable of managing multiple file descriptors simultaneously without losing context across reads.

## Compilation & Usage

### Function Prototype

```c
char *get_next_line(int fd);
```

### Integration

Include the header in your C file and compile it along with `get_next_line.c` and `get_next_line_utils.c`. You can customize the `BUFFER_SIZE` flag during compilation:

```bash
# Compilation with a default or custom BUFFER_SIZE
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 main.c get_next_line.c get_next_line_utils.c -o gnl_test
```

### Example Usage

```c
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include "get_next_line.h"

int main(void)
{
    int     fd;
    char    *line;

    fd = open("example.txt", O_RDONLY);
    if (fd < 0)
        return (1);
    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

## Allowed Functions

- `read`, `free`, `malloc`