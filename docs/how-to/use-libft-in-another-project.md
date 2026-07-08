# Use libft in another project

This guide shows how to add libft to an existing C project.

Assume the projects have this structure:

```text
workspace/
├── libft_42/
│   ├── include/
│   ├── Makefile
│   └── libft.a
└── my_project/
    ├── main.c
    └── Makefile
```

## Include the header

In your C source file, include the libft header:

```c
#include "libft.h"
```

## Compile from the command line

Build libft first:

```bash
make -C ../libft_42
```

Then compile your program:

```bash
cc main.c \
  -I../libft_42/include \
  -L../libft_42 \
  -lft \
  -o my_program
```

The options have the following purposes:

* `-I../libft_42/include` adds the libft header directory.
* `-L../libft_42` adds the directory containing `libft.a`.
* `-lft` links the program with libft.

## Add libft to a Makefile

You can also build and link libft automatically:

```makefile
NAME = my_program
CC = cc
CFLAGS = -Wall -Wextra -Werror

LIBFT_DIR = ../libft_42
LIBFT = $(LIBFT_DIR)/libft.a
INCLUDES = -I$(LIBFT_DIR)/include

SRC = main.c
OBJ = $(SRC:.c=.o)

$(NAME): $(LIBFT) $(OBJ)
	$(CC) $(OBJ) -L$(LIBFT_DIR) -lft -o $(NAME)

$(LIBFT):
	$(MAKE) -C $(LIBFT_DIR)

%.o: %.c
	$(CC) $(CFLAGS) $(INCLUDES) -c $< -o $@

clean:
	rm -f $(OBJ)

fclean: clean
	rm -f $(NAME)

re: fclean $(NAME)

.PHONY: clean fclean re
```

Run:

```bash
make
```

The Makefile builds libft when needed, compiles your project, and links the resulting program with `libft.a`.
