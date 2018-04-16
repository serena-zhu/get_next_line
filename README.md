# <a name="top">get_next_line</a>

Get_next_line is a function that reads data from a file or standard input one line at a time. This function can also handle multiple file descriptors without losing the reading thread on each of the descriptors.


## Contents

[Language & Functions Used](#language_functions) | [Prototype & Buffer Size](#prototype_buffer)

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
* the second parameter is the address of a pointer to a character that will be used to save the line (without '\n') read from the file descriptor.
* The return value will be 1, 0, or -1 depending on whether a line has been read, when the reading has been completed, or if an error has occured, respectively.

#### `Buffer Size`

A macro named BUFF_SIZE is defined in the [get_next_line.h](/get_next_line.h) file. This value can be modified as desired. 

<a href="#top">↥ back to top</a>