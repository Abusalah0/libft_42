# Function reference

This page documents the public functions declared in `include/libft.h`.

Include the header before using the library:

```c
#include "libft.h"
```

Functions marked **caller frees** return dynamically allocated memory. Release that memory with `free()` when you no longer need it.

## Character functions

| Function | Description |
|---|---|
| `int ft_isalpha(int c)` | Returns a nonzero value when `c` is an ASCII letter. |
| `int ft_isdigit(int c)` | Returns a nonzero value when `c` is a decimal digit. |
| `int ft_isalnum(int c)` | Returns a nonzero value when `c` is a letter or decimal digit. |
| `int ft_isascii(int c)` | Returns a nonzero value when `c` is within the ASCII range. |
| `int ft_isprint(int c)` | Returns a nonzero value when `c` is a printable ASCII character. |
| `int ft_isspace(int c)` | Returns a nonzero value when `c` is a whitespace character. |
| `int ft_toupper(int c)` | Converts a lowercase ASCII letter to uppercase. Other values are returned unchanged. |
| `int ft_tolower(int c)` | Converts an uppercase ASCII letter to lowercase. Other values are returned unchanged. |

## Numeric conversion and validation

| Function | Description | Ownership |
|---|---|---|
| `int ft_atoi(const char *nptr)` | Converts the beginning of a string to an `int`. | None |
| `long ft_atol(const char *str)` | Converts the beginning of a string to a `long`. | None |
| `double ft_atod(const char *s)` | Converts a decimal string to a `double`. Supports an optional sign, fractional part, and exponent. | None |
| `char *ft_itoa(int n)` | Converts an integer to a newly allocated decimal string. | Caller frees |
| `int ft_count_digits(int n)` | Returns the number of decimal digits in an integer. The sign is not counted. | None |
| `int ft_isnumber(char *str)` | Returns a nonzero value when `str` contains an optional sign followed by at least one decimal digit. | None |
| `bool ft_is_power_of_2(int num)` | Returns `true` when `num` is a positive power of two. | None |

### `ft_atod`

```c
double ft_atod(const char *s);
```

`ft_atod` accepts values such as:

```text
42
-3.14
+0.5
1.25e3
4.2E-2
```

The function does not report conversion errors separately.

## Memory functions

| Function | Description | Returned pointer |
|---|---|---|
| `void *ft_memset(void *s, int c, size_t n)` | Sets the first `n` bytes of `s` to `c`. | `s` |
| `void ft_bzero(void *s, size_t n)` | Sets the first `n` bytes of `s` to zero. | — |
| `void *ft_memcpy(void *dest, const void *src, size_t n)` | Copies `n` bytes from `src` to `dest`. The memory regions must not overlap. | `dest` |
| `void *ft_memmove(void *dest, const void *src, size_t n)` | Copies `n` bytes from `src` to `dest`. Overlapping regions are supported. | `dest` |
| `void *ft_memchr(const void *s, int c, size_t n)` | Finds the first occurrence of byte `c` within the first `n` bytes of `s`. | Borrowed pointer or `NULL` |
| `int ft_memcmp(const void *s1, const void *s2, size_t n)` | Compares the first `n` bytes of two memory regions. | — |
| `void *ft_calloc(size_t nmemb, size_t size)` | Allocates zero-initialized memory for `nmemb` elements. | Caller frees |

## String inspection and comparison

| Function | Description | Returned pointer |
|---|---|---|
| `size_t ft_strlen(const char *str)` | Returns the number of characters before the null terminator. | — |
| `char *ft_strchr(const char *s, int c)` | Finds the first occurrence of `c` in `s`. | Borrowed pointer or `NULL` |
| `char *ft_strrchr(const char *s, int c)` | Finds the last occurrence of `c` in `s`. | Borrowed pointer or `NULL` |
| `int ft_strcmp(const char *s1, const char *s2)` | Compares two null-terminated strings. Returns a negative value, zero, or a positive value. | — |
| `int ft_strncmp(const char *s1, const char *s2, size_t n)` | Compares at most `n` characters from two strings. | — |
| `char *ft_strnstr(const char *big, const char *little, size_t len)` | Finds `little` within the first `len` characters of `big`. | Borrowed pointer or `NULL` |

A borrowed pointer refers to memory inside the original string. Do not free it separately.

## String copying

| Function | Description |
|---|---|
| `char *ft_strcpy(char *dest, const char *src)` | Copies `src`, including its null terminator, into `dest`. |
| `char *ft_strncpy(char *dest, const char *src, size_t n)` | Copies at most `n` characters from `src` into `dest`. |
| `size_t ft_strlcpy(char *dest, const char *src, size_t size)` | Copies a string into a size-limited buffer and returns the length of `src`. |
| `size_t ft_strlcat(char *dest, const char *src, size_t size)` | Appends a string to a size-limited buffer and returns the total length it attempted to create. |

The destination buffer must have enough space for functions that do not receive its total capacity.

## Allocating string functions

| Function | Description | Ownership |
|---|---|---|
| `char *ft_strdup(const char *s)` | Creates a duplicate of `s`. | Caller frees |
| `char *ft_substr(const char *s, unsigned int start, size_t len)` | Creates a substring beginning at `start`. | Caller frees |
| `char *ft_strjoin(const char *s1, const char *s2)` | Creates a string containing `s1` followed by `s2`. | Caller frees |
| `char *ft_strtrim(const char *s1, const char *set)` | Removes characters from `set` from both ends of `s1`. | Caller frees |
| `char *ft_strmapi(const char *s, char (*f)(unsigned int, char))` | Creates a string by applying `f` to every character in `s`. | Caller frees |
| `char *ft_str_replace(const char *str, const char *old, const char *new)` | Creates a string in which every non-overlapping occurrence of `old` is replaced with `new`. | Caller frees |

All these functions return `NULL` when allocation fails.

## String modification

### `ft_striteri`

```c
void ft_striteri(char *s, void (*f)(unsigned int, char *));
```

Applies `f` to every character in `s`.

The callback receives:

- the character index,
- a pointer to the character.

The callback can modify the original string.

## String splitting

### `ft_split`

```c
char **ft_split(const char *s, char c);
```

Splits `s` using `c` as the delimiter.

The returned value is a null-terminated array of newly allocated strings.

Example:

```c
char **parts;

parts = ft_split("one:two:three", ':');
```

The result contains:

```text
parts[0] -> "one"
parts[1] -> "two"
parts[2] -> "three"
parts[3] -> NULL
```

Free each string before freeing the array:

```c
size_t i;

i = 0;
while (parts[i] != NULL)
{
    free(parts[i]);
    i++;
}
free(parts);
```

## File-descriptor output

| Function | Description |
|---|---|
| `void ft_putchar_fd(char c, int fd)` | Writes one character to `fd`. |
| `void ft_putstr_fd(char *s, int fd)` | Writes a null-terminated string to `fd`. |
| `void ft_putendl_fd(char *s, int fd)` | Writes a string followed by a newline to `fd`. |
| `void ft_putnbr_fd(int n, int fd)` | Writes the decimal representation of an integer to `fd`. |

Common file descriptors are:

| File descriptor | Stream |
|---:|---|
| `0` | Standard input |
| `1` | Standard output |
| `2` | Standard error |

## Line input

### `get_next_line`

```c
char *get_next_line(int fd);
```

Reads and returns the next line from `fd`.

The returned line includes the newline character when one was read. The final line may not contain a newline.

**Return value:**

- a newly allocated line on success,
- `NULL` at the end of the file,
- `NULL` when reading or allocation fails.

The caller must free every returned line.

```c
char *line;

line = get_next_line(fd);
while (line != NULL)
{
    ft_putstr_fd(line, 1);
    free(line);
    line = get_next_line(fd);
}
```

`BUFFER_SIZE` controls the read-buffer size. Its default value is `1024`, but you can override it during compilation:

```bash
cc -D BUFFER_SIZE=4096 ...
```

## Linked-list type

The linked-list functions use the following type:

```c
typedef struct s_list
{
    void            *content;
    struct s_list   *next;
} t_list;
```

Build the linked-list functions with:

```bash
make bonus
```

## Linked-list functions

| Function | Description |
|---|---|
| `t_list *ft_lstnew(void *content)` | Allocates a new node containing `content`. |
| `void ft_lstadd_front(t_list **lst, t_list *new_node)` | Adds a node to the beginning of a list. |
| `void ft_lstadd_back(t_list **lst, t_list *new_node)` | Adds a node to the end of a list. |
| `t_list *ft_lstlast(t_list *lst)` | Returns the final node in a list. |
| `int ft_lstsize(t_list *lst)` | Returns the number of nodes in a list. |
| `void ft_lstdelone(t_list *lst, void (*del)(void *))` | Deletes one node and releases its content with `del`. |
| `void ft_lstclear(t_list **lst, void (*del)(void *))` | Deletes every node and sets the list pointer to `NULL`. |
| `void ft_lstiter(t_list *lst, void (*f)(void *))` | Applies `f` to the content of every node. |
| `t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *))` | Creates a new list by applying `f` to each node’s content. |

`ft_lstnew` stores the content pointer directly. It does not copy the object referenced by that pointer.