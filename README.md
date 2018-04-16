# <a name="top">get_next_line</a>

Get_next_line is a function that reads data from a file or standard input one line at a time. A line is a succession of characters that end with '\n'. This function can also handle multiple file descriptors without losing the reading thread on each of the descriptors.


## Contents

[Language & Functions Used](#language_functions) | [Prototype & Buffer Size](#prototype_buffer) | [Example](#example)

## <a name="language_functions">Language & Functions Used</a>

The fdf program is written in C, using only the following functions from the standard C libraries:

* read
* malloc
* free

<a href="#top">↥ back to top</a>

## <a name="prototype_buffer">Prototype & Buffer Size</a>

#### `Prototype`

```
int      get_next_line(const int fd, char **line);	
```

* The first parameter is the file descriptor that will be used to read.
* The second parameter is the address of a pointer to a character that will be used to save the line (without '\n') read from the file descriptor.
* The return value will be 1, 0, or -1 depending on whether a line has been read, when the reading has been completed, or if an error has occured, respectively.

#### `Buffer Size`

A macro named BUFF_SIZE is defined in the [get_next_line.h](/get_next_line.h) file. This value can be modified as desired. 

<a href="#top">↥ back to top</a>

## <a name="example">Example</a>

```bash
$ cat lorem_ipsum.txt
Line 1 - Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
Line 2 - Ut pellentesque, mauris et egestas pulvinar, elit turpis dapibus mauris, et aliquet purus lectus non metus.
Line 3 - Sed sit amet leo commodo, egestas tellus at, consequat neque.
Line 4 - Nunc sed venenatis sapien, sit amet pharetra lacus.
Line 5 - Nam eu tincidunt est. 
Line 6 - Aenean sodales sagittis scelerisque.
Line 7 - Duis maximus risus sit amet ipsum sollicitudin, et tempor velit scelerisque.
Line 8 - Etiam gravida sem nulla, quis vulputate libero aliquet sit amet. 
Line 9 - Duis tempus convallis eleifend.
$ cat main.c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int	main(int argc, char **argv)
{
	char *line;
	int fd;
	int fd2;
	int result;
	int	i;

	if (argc > 1)
	{
		i = 0;
		fd = open(argv[1], O_RDONLY);
		fd2 = open(argv[1], O_RDONLY);
		while ((result = get_next_line(fd, &line)) == 1)
		{
			printf("fd: %d, %s\n", fd, line);
			free(line);
			i++;
			if (i % 2 == 0 && (result = get_next_line(fd2, &line)) == 1)
			{
				printf("fd: %d, %s\n", fd2, line);
				free(line);
			}
		}
		close(fd);
		close(fd2);
	}
	return (0);
}
$ gcc -Wall -Wextra -Werror main.c get_next_line.c libft/*.c
$ ./a.out lorem_ipsum.txt
fd: 3, Line 1 - Lorem ipsum dolor sit amet, consectetur adipiscing elit.
fd: 3, Line 2 - Ut pellentesque, mauris et egestas pulvinar, elit turpis dapibus mauris, et aliquet purus lectus non metus.
fd: 4, Line 1 - Lorem ipsum dolor sit amet, consectetur adipiscing elit.
fd: 3, Line 3 - Sed sit amet leo commodo, egestas tellus at, consequat neque.
fd: 3, Line 4 - Nunc sed venenatis sapien, sit amet pharetra lacus.
fd: 4, Line 2 - Ut pellentesque, mauris et egestas pulvinar, elit turpis dapibus mauris, et aliquet purus lectus non metus.
fd: 3, Line 5 - Nam eu tincidunt est.
fd: 3, Line 6 - Aenean sodales sagittis scelerisque.
fd: 4, Line 3 - Sed sit amet leo commodo, egestas tellus at, consequat neque.
fd: 3, Line 7 - Duis maximus risus sit amet ipsum sollicitudin, et tempor velit scelerisque.
fd: 3, Line 8 - Etiam gravida sem nulla, quis vulputate libero aliquet sit amet.
fd: 4, Line 4 - Nunc sed venenatis sapien, sit amet pharetra lacus.
fd: 3, Line 9 - Duis tempus convallis eleifend.
```

<a href="#top">↥ back to top</a>
