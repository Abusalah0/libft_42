# Contributing to libft

Thank you for your interest in contributing to libft.

This project welcomes focused bug fixes, tests, documentation improvements, and changes that improve correctness or maintainability without unnecessarily expanding the library.

## Before you start

For significant changes, open an issue before writing code. Describe:

- the problem you want to solve,
- the proposed behavior,
- why the change belongs in libft,
- and any alternatives you considered.

Small fixes, such as typo corrections or narrowly scoped bug fixes, may be submitted directly as a pull request.

Do not use public issues to report security vulnerabilities. Follow the instructions in [`SECURITY.md`](SECURITY.md).

## Development setup

You need:

- Git,
- Make,
- a C compiler such as `cc`, `clang`, or `gcc`.

Clone your fork:

```sh
git clone https://github.com/YOUR_USERNAME/libft_42.git
cd libft_42
````

Add the original repository as an upstream remote:

```sh
git remote add upstream https://github.com/Abusalah0/libft_42.git
git fetch upstream
```

Create a branch from the latest default branch:

```sh
git switch master
git pull --ff-only upstream master
git switch -c fix/short-description
```

Use a descriptive branch name, such as:

```text
fix/strcmp-return-type
test/split-empty-input
docs/improve-memory-ownership
```

## Repository structure

The main project files are organized as follows:

```text
include/       Public headers
src/           Function implementations
docs/          Project documentation
Makefile       Library build rules
mkdocs.yml     Documentation site configuration
```

Public functions must be declared in `include/libft.h`.

## Build the project

Build the main library:

```sh
make
```

This creates:

```text
libft.a
```

Build the linked-list functions:

```sh
make bonus
```

Rebuild everything from a clean state:

```sh
make re
```

Remove generated object files:

```sh
make clean
```

Remove object files and the library:

```sh
make fclean
```

The project must compile without warnings.

## Test your changes

Before submitting a pull request, build the project from a clean state:

```sh
make fclean
make
make bonus
```

Test both normal behavior and relevant edge cases.

For bug fixes, include a small reproducer or test that:

1. fails before the change,
2. passes after the change,
3. exercises the exact behavior being fixed.

Useful tools for memory-related changes include:

```sh
valgrind --leak-check=full ./your_test_program
```

or compiler sanitizers:

```sh
cc -Wall -Wextra -Werror \
  -fsanitize=address,undefined \
  -Iinclude \
  your_test_program.c \
  -L. -lft \
  -o your_test_program
```

Do not commit generated executables, object files, profiler output, or temporary test artifacts.

## Code style

Follow the existing project style.

In particular:

- compile with `-Wall -Wextra -Werror`,
- keep functions focused,
- use clear names,
- avoid unrelated formatting changes,
- preserve existing public behavior unless the change is intentional and documented,
- handle allocation failures,
- document memory ownership when adding functions that return pointers.

Do not mix refactoring with an unrelated bug fix. Separate changes are easier to review and safer to merge.

## Documentation changes

Update the documentation when changing:

- a public function,
- a function prototype,
- return-value behavior,
- memory ownership,
- supported inputs,
- build or integration instructions.

Preview the documentation locally with:

```sh
mkdocs serve
```

Validate the production build with:

```sh
mkdocs build --strict
```

## Filing a bug report

Use the bug-report issue form and include:

- a clear description of the problem,
- expected and actual behavior,
- the smallest program that reproduces it,
- the affected version or commit,
- your compiler and operating system,
- relevant sanitizer, Valgrind, or debugger output.

A minimal reproducer is more useful than a full project.

## Pull request conventions

Keep each pull request focused on one logical change.

A pull request should include:

- what changed,
- why the change is needed,
- how it was tested,
- any compatibility or ownership implications,
- a linked issue when applicable.

Use clear commit messages. Examples:

```text
fix: correct signed result from ft_strcmp
test: cover sign-only input in ft_isnumber
docs: clarify ft_split ownership
```

Before opening the pull request:

```sh
git diff --check
make fclean
make
make bonus
```

Review the complete diff and remove unrelated changes.

## Review expectations

Pull requests are reviewed for:

- correctness,
- compatibility with the existing API,
- memory safety,
- focused scope,
- adequate testing,
- documentation accuracy,
- consistency with the project style.

Review feedback may request changes before merging. Address comments with new commits while the review is active. Avoid force-pushing after review has started unless rewriting the branch is necessary and clearly communicated.

Approval is not guaranteed. A technically correct change may still be declined when it adds unnecessary API surface, increases maintenance cost, or does not fit the project’s direction.

## License

By contributing, you agree that your contribution will be licensed under the same license as this repository.
