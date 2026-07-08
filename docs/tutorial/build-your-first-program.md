# Build your first program with libft

This tutorial is for C developers who have Git, Make, and a C compiler installed.

By the end of this tutorial, you will build libft and use it in a small C program.

## Clone the repository

```bash
git clone https://github.com/Abusalah0/libft_42.git
cd libft_42
```

The repository contains:

* `include/libft.h`, which declares the public functions.
* `src/`, which contains the implementations.
* `Makefile`, which builds the library.

## Build the library

Run:

```bash
make
```

This command creates the static library:

```text
libft.a
```

## Create a program

Create a file named `hello.c`:

```c
#include "libft.h"

int main(void)
{
    ft_putstr_fd("Hello, World!\n", 1);
    return (0);
}
```

The second argument to `ft_putstr_fd` is the file descriptor. File descriptor `1` represents standard output.

## Compile the program

Run:

```bash
cc hello.c -Iinclude -L. -lft -o hello
```

The options mean:

* `-Iinclude` tells the compiler where to find `libft.h`.
* `-L.` tells the linker where to find `libft.a`.
* `-lft` links the program with libft.
* `-o hello` names the executable `hello`.

## Run the program

```bash
./hello
```

You should see:

```text
Hello, World!
```

You have now built libft and linked it to a C program. See the function reference for the other available functions.
