<!-- omit in toc -->
# Development Info

This document serves as a comprehensive guide to various aspects of project development, including versioning, style guidelines, and recommended practices.

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

Versioning is a pivotal aspect of our project's evolution. Our versioning scheme
adopts the format:

```none
FullYear.Version.BugFix
```

This approach draws inspiration from Intellij versioning, calendar versioning,
and semantic versioning. Combining their strengths:

- Year Indication: Actively indicates ongoing development.
- Frequent Releases: Multiple versions within a year.
- Bugfix Clarity: Bugfixes do not result in new version increments.

Prominent projects adhering to similar schemes include:

- Unity
- PyCharm
- Spring Cloud

Note that slight variations, like the short year format, are present in projects
like Python PIP.

## Style Guides

### General

While our primary guide is the official style guide of each language, exceptions
are necessary for cohesion. Notable modifications include:

- **Indentation**: Utilize a single hard tab (`\t`) for a 4-character indentation
  wherever possible.
- **Maximum Line Length**: Opt for a maximum line length of 100 characters whenever
  feasible. Exceptions may arise, such as with URLs exceeding 100 characters.

### Python

Comply with https://www.python.org/dev/peps/pep-0008/ while integrating the
modifications mentioned in [General](#general). Additionally:

- **Variable, Function, and Argument Names**: Employ camel case (e.g., `camelCase`).
- **Comments/Documentation**: Utilize the Google DocString style.

#### Pre-commit (Python)

To ensure adherence to the Python style guide and perform valuable checks, employ the following `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/FHPythonUtils/Blackt
    rev: '2022.0.3'
    hooks:
      - id: blackt

  - repo: https://github.com/pycqa/isort
    rev: 5.12.0
    hooks:
      - id: isort

  - repo: https://github.com/pycqa/pylint
    rev: v3.0.0a6
    hooks:
      - id: pylint
        exclude: "tests/"
        args: [--disable=import-error,--jobs=0]

  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
        exclude: "tests/"
      - id: end-of-file-fixer
        exclude: "tests/"

  - repo: https://github.com/asottile/pyupgrade
    rev: v3.7.0
    hooks:
      - id: pyupgrade
        args: [--py38-plus]
  - repo: https://github.com/boidolr/pre-commit-images
    rev: v1.2.1
    hooks:
      - id: optimize-avif
        exclude: "tests/"
      - id: optimize-jpg
        exclude: "tests/"
      - id: optimize-png
        exclude: "tests/"
      - id: optimize-svg
        exclude: "tests/"
      - id: optimize-webp
        exclude: "tests/"
```

Use the provided configuration snippet in your `pyproject.toml`:

```toml
[tool.black]
line-length = 100
target-version = ["py38"]

[tool.isort]
profile = "black"
indent = "Tab"

[tool.pydocstyle]
convention = "google"
ignore = "D205,D415"

[tool.pylint.basic]
argument-naming-style = "camelCase"
attr-naming-style = "camelCase"
function-naming-style = "camelCase"
method-naming-style = "camelCase"
variable-naming-style = "camelCase"

[tool.pylint.format]
indent-string = "\t"

[tool.pylint.master]
ignore-paths = ["tests"]

[tool.pylint.messages_control]
enable = ["F", "E", "W", "R", "C"]
disable = ["pointless-string-statement", "superfluous-parens"]

```

### Kotlin

Align with https://kotlinlang.org/docs/coding-conventions.html while factoring
in the guidelines established in [General](#general).

#### Pre-commit (Kotlin)

Coming soon

### Java

Adopt https://google.github.io/styleguide/javaguide.html while incorporating the
adjustments outlined in [General](#general). Additionally:

- **File Names**: Embrace pascal case (e.g., `PascalCase`).

#### Pre-commit (Java)

Coming soon
