# libft_42

A static C library that re-implements core libc behavior and adds utility helpers commonly used in 42 projects.

This project builds into libft.a and includes:

- Character and numeric helpers
- Memory operations
- String utilities
- File descriptor output helpers
- A get_next_line implementation
- Bonus singly linked list utilities

## Why use this library

- Provides a reusable base for C projects
- Keeps common operations in one tested archive
- Follows 42-style modular organization
- Easy to integrate with any C program through a single static library

## Repository layout

```text
include/
  libft.h
src/
  int_ops/
  memory/
  string/
  print/
  input/
  linked_lst/      (bonus)
Makefile
```

## Build

From the project root:

```bash
make
```

This creates:

- libft.a with the base library objects

Available Makefile targets:

- make: build base library
- make bonus: build base + linked list bonus sources
- make clean: remove object files
- make fclean: remove object files and libft.a
- make re: full rebuild

## Install in another project

### Option 1: as a git subdirectory

```bash
git clone https://github.com/Abusalah0/libft_42.git
cd libft_42
make
```

Then link from your project:

```bash
cc main.c -I/path/to/libft_42/include -L/path/to/libft_42 -lft
```

### Option 2: with direct archive path

```bash
cc main.c /path/to/libft_42/libft.a -I/path/to/libft_42/include
```

## Public API overview

Header: include/libft.h

### Character and integer helpers

- ft_isalpha, ft_isdigit, ft_isalnum, ft_isascii, ft_isprint, ft_isspace
- ft_toupper, ft_tolower
- ft_atoi, ft_atol, ft_atod
- ft_itoa, ft_count_digits, ft_isnumber, ft_is_power_of_2

### Memory

- ft_memset, ft_bzero, ft_memcpy, ft_memmove
- ft_memchr, ft_memcmp, ft_calloc

### Strings

- ft_strlen, ft_strdup, ft_strcpy, ft_strncpy
- ft_strchr, ft_strrchr, ft_strncmp, ft_strcmp, ft_strnstr
- ft_strlcpy, ft_strlcat
- ft_substr, ft_strjoin, ft_strtrim, ft_split
- ft_strmapi, ft_striteri, ft_str_replace

### Output

- ft_putchar_fd, ft_putstr_fd, ft_putendl_fd, ft_putnbr_fd

### Input

- get_next_line

### Bonus linked list

- t_list
- ft_lstnew, ft_lstadd_front, ft_lstadd_back, ft_lstlast, ft_lstsize
- ft_lstdelone, ft_lstclear, ft_lstiter, ft_lstmap

## Quick usage examples

### String split example

```c
#include "libft.h"
#include <stdio.h>

int main(void)
{
	char **parts = ft_split("42:libft:example", ':');
	int i = 0;

	while (parts && parts[i])
	{
		printf("%s\n", parts[i]);
		free(parts[i]);
		i++;
	}
	free(parts);
	return (0);
}
```

### get_next_line example

```c
#include "libft.h"
#include <fcntl.h>

int main(void)
{
	int fd = open("input.txt", O_RDONLY);
	char *line;

	if (fd < 0)
		return (1);
	line = get_next_line(fd);
	while (line)
	{
		ft_putstr_fd(line, 1);
		free(line);
		line = get_next_line(fd);
	}
	close(fd);
	return (0);
}
```

## Notes

- BUFFER_SIZE for get_next_line defaults to 1024 and can be overridden at compile time.
- The project is intended as a reusable base library for 42 C projects.
- Code style targets 42 Norm conventions.
