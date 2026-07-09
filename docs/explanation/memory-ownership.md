# Memory ownership in libft

C does not manage dynamically allocated memory for you. When a function allocates memory, your program must eventually release it with `free()`.

To use libft safely, you need to know whether a returned pointer refers to:

- newly allocated memory,
- memory owned by another object,
- or a collection containing several allocations.

## Owned and borrowed memory

An **owned pointer** refers to memory that your code is responsible for releasing.

A **borrowed pointer** refers to memory owned elsewhere. You may use the pointer while the original memory remains valid, but you must not free it separately.

Consider the following example:

```c
char *copy;

copy = ft_strdup("libft");
if (copy == NULL)
    return (1);

free(copy);
````

`ft_strdup` creates a new string. The returned pointer owns a separate allocation, so the caller must free it.

By contrast, `ft_strchr` returns a pointer into an existing string:

```c
char text[] = "libft";
char *match;

match = ft_strchr(text, 'f');
```

`match` points to part of `text`. It does not refer to a new allocation.

Do not call:

```c
free(match);
```

The original array owns that memory.

## Functions that allocate memory

Several libft functions return newly allocated memory:

- `ft_calloc`
- `ft_strdup`
- `ft_substr`
- `ft_strjoin`
- `ft_strtrim`
- `ft_split`
- `ft_itoa`
- `ft_strmapi`

Check the result before using it because allocation can fail:

```c
char *result;

result = ft_strjoin("lib", "ft");
if (result == NULL)
    return (1);

ft_putstr_fd(result, 1);
free(result);
```

Free each successful allocation exactly once.

## Functions that return borrowed pointers

Some functions search existing memory and return a pointer into it:

- `ft_strchr`
- `ft_strrchr`
- `ft_memchr`

For example:

```c
char text[] = "hello";
char *result;

result = ft_strchr(text, 'e');
if (result != NULL)
    ft_putstr_fd(result, 1);
```

`result` points to the second character of `text`. It remains valid only while `text` remains valid.

If the original memory is freed or goes out of scope, the borrowed pointer becomes invalid.

## Nested allocations from `ft_split`

`ft_split` creates more than one allocation. It allocates:

1. an array of string pointers,
2. one string for each part,
3. a final null pointer that marks the end of the array.

```c
char **parts;

parts = ft_split("one:two:three", ':');
if (parts == NULL)
    return (1);
```

Free every string before freeing the array:

```c
void free_split(char **parts)
{
    size_t i;

    if (parts == NULL)
        return;
    i = 0;
    while (parts[i] != NULL)
    {
        free(parts[i]);
        i++;
    }
    free(parts);
}
```

You can then use the helper after processing the result:

```c
parts = ft_split("one:two:three", ':');
if (parts == NULL)
    return (1);

/* Use parts. */

free_split(parts);
```

Freeing only the array leaks the individual strings. Freeing only the strings leaks the array.

## Linked-list ownership

A linked-list node and its content are separate values.

`ft_lstnew` allocates a new node, but it does not copy the content passed to it:

```c
char *content;
t_list *node;

content = ft_strdup("libft");
if (content == NULL)
    return (1);

node = ft_lstnew(content);
if (node == NULL)
{
    free(content);
    return (1);
}
```

In this example, the program allocates both `content` and `node`.

When deleting the node, provide a function that releases its content:

```c
ft_lstdelone(node, free);
```

The deletion function determines how the content is cleaned up. This allows list nodes to contain dynamically allocated data, static data, or other objects with custom cleanup requirements.

## Common ownership mistakes

### Memory leak

A memory leak occurs when your program loses the last pointer to an allocation without freeing it.

```c
char *text;

text = ft_strdup("first");
text = ft_strdup("second");
```

The second assignment replaces the only pointer to the first allocation.

Free the first value before replacing it:

```c
text = ft_strdup("first");
if (text == NULL)
    return (1);

free(text);
text = ft_strdup("second");
```

### Double free

A double free occurs when your program releases the same allocation more than once.

```c
free(text);
free(text);
```

After freeing a pointer, you can assign `NULL` to it when the pointer may be reused:

```c
free(text);
text = NULL;
```

Calling `free(NULL)` is valid.

### Freeing borrowed memory

Do not free pointers returned inside existing strings or buffers:

```c
match = ft_strchr(text, 'x');
free(match);
```

`match` does not own a separate allocation.

### Use after free

A pointer becomes invalid after its allocation is released:

```c
free(text);
ft_putstr_fd(text, 1);
```

Do not read from or write to freed memory.

## Ownership checklist

Before using a returned pointer, ask:

1. Did the function allocate new memory?
2. Who is responsible for freeing it?
3. Does the value contain nested allocations?
4. How long does the original memory remain valid?
5. What cleanup is required when an operation fails?

Answering these questions helps prevent memory leaks, double frees, and invalid memory access.
