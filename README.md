# mdformat-tight-lists

[![Build Status][ci-badge]][ci-link]
[![codecov.io][cov-badge]][cov-link]
[![PyPI version][pypi-badge]][pypi-link]

An opinionated [mdformat](https://github.com/executablebooks/mdformat) plugin that aggressively formats lists to be tight (no empty lines between list items).

**Note**: This plugin takes an opinionated stance that most lists should be tight lists. It will convert loose lists (with empty lines between items) to tight lists, which changes the rendered HTML output. The plugin requires mdformat to be run with the `--no-validate` flag to bypass HTML validation checks.

## Installation

```bash
pip install mdformat-tight-lists
```

or with [pipx](https://pipx.pypa.io/):

```bash
pipx install mdformat
pipx inject mdformat mdformat-tight-lists
```

## Usage

### Shell Command

Since mdformat-tight-lists is an opinionated plugin that greedily converts loose lists to tight lists and potentially changes the semantics of HTML output, mdformat with this plugin installed should be run with the `--no-validate` flag to avoid seeing mdformat's validation errors. 

After installation, use mdformat to apply tight-list formatting to Markdown files:

```bash
# Add the option manually
mdformat --no-validate your-file.md

# Create an alias for persistence
alias mdformat="mdformat --no-validate"
```

### Features

- **Aggressive Tight Formatting**: Converts loose lists to tight lists by removing empty lines between list items
- **Multi-Paragraph Exception**: Only preserves loose formatting when list items contain multiple paragraphs
- **Opinionated Approach**: Believes most lists should be tight lists - paragraph tags around every list item in HTML is excessive
- **HTML Semantic Changes**: This plugin intentionally changes HTML output (loose to tight lists), requiring `--no-validate` flag

### Examples

**Input:**
```markdown
- Item 1

- Item 2

- Item 3
```

**Output:**
```markdown
- Item 1
- Item 2
- Item 3
```

**Multi-paragraph items (loose list preserved):**
```markdown
- First item with multiple paragraphs

  Second paragraph of first item

- Second item
```

## Development

This package utilises [flit](https://flit.readthedocs.io) as the build engine, and [tox](https://tox.readthedocs.io) for test automation.

To install these development dependencies:

```bash
pip install tox
```

To run the tests:

```bash
tox
```

and with test coverage:

```bash
tox -e py37-cov
```

The easiest way to write tests, is to edit tests/fixtures.md

To run the code formatting and style checks:

```bash
tox -e py37-pre-commit
```

or directly

```bash
pip install pre-commit
pre-commit run --all
```

To run the pre-commit hook test:

```bash
tox -e py37-hook
```

## Publish to PyPi

Either use flit directly:

```bash
pip install flit
flit publish
```

or trigger the GitHub Action job, by creating a release with a tag equal to the version, e.g. `v0.0.1`.

Note, this requires generating an API key on PyPi and adding it to the repository `Settings/Secrets`, under the name `PYPI_KEY`.

[ci-badge]: https://github.com/jdmonaco/mdformat-tight-lists/workflows/CI/badge.svg?branch=master
[ci-link]: https://github.com/jdmonaco/mdformat-tight-lists/actions?query=workflow%3ACI+branch%3Amaster+event%3Apush
[cov-badge]: https://codecov.io/gh/jdmonaco/mdformat-tight-lists/branch/master/graph/badge.svg
[cov-link]: https://codecov.io/gh/jdmonaco/mdformat-tight-lists
[pypi-badge]: https://img.shields.io/pypi/v/mdformat-tight-lists.svg
[pypi-link]: https://pypi.org/project/mdformat-tight-lists

