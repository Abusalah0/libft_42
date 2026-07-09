# 0001. Use MkDocs Material for project documentation

## Status

Accepted, 2026-07-09.

## Context

The libft repository needs documentation that is easier to navigate than a single README file.

The documentation includes different types of content:

- a tutorial for new users,
- how-to guides for specific tasks,
- a function reference,
- explanations of C and libft concepts.

The documentation should remain close to the source code so changes can be reviewed and versioned through Git.

The project needs a documentation system that:

- uses Markdown,
- requires little configuration,
- provides clear navigation,
- supports local previews,
- generates a static website,
- and can deploy to GitHub Pages.

The alternatives considered were:

- keeping all documentation in `README.md`,
- using mdBook,
- using Docusaurus,
- and using MkDocs Material.

## Decision

The project will use MkDocs Material.

Documentation source files will be stored under `docs/`, and the site configuration will be stored in `mkdocs.yml`.

The documentation will follow the Diátaxis structure:

- tutorials,
- how-to guides,
- reference documentation,
- explanations.

The generated site will be published through GitHub Pages.

## Consequences

### Positive consequences

- Contributors can write documentation in Markdown.
- Documentation changes can use the same Git workflow as code changes.
- MkDocs provides local previews with automatic reloading.
- Material provides navigation, search, and readable default styling.
- The generated site can be hosted as a static GitHub Pages website.
- The documentation can grow without making the README difficult to navigate.

### Negative consequences

- Contributors need MkDocs to preview the site locally.
- The project must maintain `mkdocs.yml` and its documentation dependencies.
- Publishing with `mkdocs gh-deploy` requires a separate deployment step.
- The generated `gh-pages` branch must not be edited manually.

## Alternatives considered

### Keep all documentation in the README

This approach requires no additional tooling, but the README becomes difficult to navigate as the documentation grows. It also makes it harder to separate tutorials, guides, reference material, and explanations.

### Use mdBook

mdBook provides a good experience for structured technical books. However, MkDocs Material provides stronger built-in navigation and search for a small documentation website.

### Use Docusaurus

Docusaurus supports advanced features and React components. Those features add unnecessary complexity for documentation consisting primarily of Markdown files.

## References

- [MkDocs documentation](https://www.mkdocs.org/)
- [Material for MkDocs documentation](https://squidfunk.github.io/mkdocs-material/)
- [Diátaxis documentation framework](https://diataxis.fr/)