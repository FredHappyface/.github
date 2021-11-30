<!-- omit in toc -->
# Development Info

This document acts as a guide to various processes regarding projects such as
the versioning scheme and the programming styles used.

- [Versioning](#versioning)
- [Style Guides](#style-guides)
	- [General](#general)
	- [Python](#python)
		- [Pre-commit (Python)](#pre-commit-python)
	- [Kotlin](#kotlin)
		- [Pre-commit (Kotlin)](#pre-commit-kotlin)
	- [Java](#java)
		- [Pre-commit (Java)](#pre-commit-java)

## Versioning

[![CalVer](https://img.shields.io/badge/calver-YYYY.Minor.Micro-22bfda.svg?style=for-the-badge)](https://pypi.org/project/[project-name]/)

Versioning is most often done as follows:

```none
FullYear.Version.BugFix
```

Inspiration is taken from Intellij versioning, calendar versioning and semantic
versioning and aims to combine the advantages of each. Those being:

- The year gives an indication of if the project is still actively developed
- Multiple versions each year
- Bugfixes are not new versions

Notable projects using this scheme (according to https://calver.org/users.html):

- Unity
- PyCharm
- Spring Cloud

A few other popular projects such as Python PIP use a slightly different
version of this with the short year.

## Style Guides

### General

The official style guide for each language should be followed whenever possible.
With the following exceptions:

- **Indentation** One hard tab (`\t`) is used for indentation with a size of 4
  where possible.
- **Maximum Line Length** A maximum line length of 100 should be used where
  possible. An example of a case where this may not be possible would be where
  there is a URL that extends 100 characters.

### Python

Follow https://www.python.org/dev/peps/pep-0008/ with the modifications defined in [General](#general) plus:

- **Variable Names** should be in camel case. e.g. `camelCase`
- **Function Names** should be in camel case. e.g. `camelCase`
- **Argument Names** should be in camel case. e.g. `camelCase`
- **Comments/ Documentation** must be in the Google DocString style

#### Pre-commit (Python)

To enforce the python styleguide, and perform a series of useful checks. The following
`.pre-commit-config.yaml` can be used. Dont forget to add the below configuration to
the `pyproject.toml`

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.0.1
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer

  - repo: https://github.com/FHPythonUtils/Blackt
    rev: '2021'
    hooks:
      - id: blackt

  - repo: https://github.com/pycqa/isort
    rev: 5.9.3
    hooks:
      - id: isort

  - repo: https://github.com/pycqa/pylint
    rev: v2.11.1
    hooks:
      - id: pylint
        args: [--disable=import-error,--jobs=0, --fail-under=9.8, --ignore-patterns=test.*?py]

  - repo: https://github.com/asottile/pyupgrade
    rev: v2.29.0
    hooks:
      - id: pyupgrade
        args: [--py37-plus]
```

Use the following configuration (add to `pyproject.toml`):

```toml
[tool.pylint.basic]
argument-naming-style = "camelCase"
attr-naming-style = "camelCase"
function-naming-style = "camelCase"
method-naming-style = "camelCase"
variable-naming-style = "camelCase"

[tool.pylint.format]
indent-string = "\t"

[tool.pylint.master]
ignore-patterns = "test_.*?py"

[tool.pylint.messages_control]
enable = ["F", "E", "W", "R", "C"]
disable = [
	"pointless-string-statement",
	"superfluous-parens",
	"bad-continuation"
]

[tool.black]
line-length = 100
target-version = ["py37"]

[tool.isort]
profile = "black"
indent = "Tab"

[tool.pydocstyle]
convention = "google"
ignore = "D205,D415"
```

### Kotlin

Follow https://kotlinlang.org/docs/coding-conventions.html with the modifications defined in [General](#general)

#### Pre-commit (Kotlin)

coming soon

### Java

Follow https://google.github.io/styleguide/javaguide.html with the modifications defined in [General](#general) plus:

- **File Names** should be in pascal case. e.g. `PascalCase` (defined https://google.github.io/styleguide/javaguide.html#s2.1-file-name)

#### Pre-commit (Java)

coming soon
