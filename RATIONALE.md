<!-- omit in toc -->
# Rationale

The rationale acts as a guide to various processes regarding projects such as
the versioning scheme and the programming styles used.

- [Versioning](#versioning)
- [Programming Style Guide](#programming-style-guide)
	- [General](#general)
	- [Python](#python)
	- [Java](#java)
- [Enforcing the style guide](#enforcing-the-style-guide)
	- [Python](#python-1)
		- [Native](#native)
		- [VSCode](#vscode)


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

## Programming Style Guide

### General

Unless specified otherwise under the language appropriate subheading (e.g.
'Python' for programming in the Python language versions 2.x and 3.x) the
following programming style guide is followed. Note that this guide is
based upon PEP8 so where this guide does not define a rule, then refer to
[PEP8](https://www.python.org/dev/peps/pep-0008/).


**Indentation** One hard tab (`\t`) is used for indentation with a size of 4
where possible.

**Maximum Line Length** A maximum line length of 80 should be used where
possible. An example of a case where this may not be possible would be where
there is a URL that extends 80 characters.

**Line Breaks** Lines should break after an operator in many cases. e.g.
```python
a = (
	b +
	c
)
```

**Blank Lines** A maximum of two consecutive blank lines should be used between
functions/ classes. A maximum of one blank line should be used inside a class.

**File Encoding** Files must be encoded as UTF-8

**Imports** Discrete modules/ dependencies must exist on separate lines. e.g.
```python
import a
from b import c
```

**Strings** If supported by the language, strings must be double-quoted (")

**Whitespace** Lines must have no trailing whitespace, files must end with a
newline. A space must follow a comma with the exception of a comma immediately
before a closing bracket/ parenthesis. e.g.
```python
def myFunction(a, b):
	...
def myFunction(a, b,):
	...
```

**Trailing Commas** Are optional but are not recommended.

**Comments/ Documentation** varies for each language though they typically
follow some basic principles.
- Document Files, Classes and Functions
- Provide a sentence to a paragraph providing a high level description of the
  function or class
- For each parameter (for functions and classes), supply the data type and
  a short description
- (optional) document lines of note. For example add a line describing or
  explaining code that may not be clear.

**File Names** should be in camel case. e.g. `camelCase`

**Class Names** should be in pascal case. e.g. `PascalCase`

**Exception Names** should be in pascal case and have a suffix `Exception`.
e.g. `PascalCaseException`

**Constant Names** should be in block caps separated by an underscore. e.g.
`BLOCK_CAPS`

**Variable Names** should be in camel case. e.g. `camelCase`

**Function Names** should be in camel case. e.g. `camelCase`

**Argument Names** should be in camel case. e.g. `camelCase`

### Python


**Comments/ Documentation** as above + must be in the Google DocString style

**File Names** should be in lower case. e.g. `lowercase`


### Java

**File Names** should be in pascal case. e.g. `PascalCase`

## Enforcing the style guide

### Python

Use `bandit`, `pylint` and `black` with the following settings:

#### Native
bandit

```cmd
python -m bandit -li --exclude **/test_*.py -s B322 -r -q .
```

pylint
```cmd
pylint --disable='pointless-string-statement, superfluous-parens, bad-continuation, wrong-import-position, unsubscriptable-object, python3' --indent-string="\t" --ignore-patterns=test_.*?py --argument-naming-style=camelCase --attr-naming-style=camelCase --function-naming-style=camelCase --method-naming-style=camelCase --variable-naming-style=camelCase --load-plugins=pylint.extensions.bad_builtin,pylint.extensions.check_elif,pylint.extensions.redefined_variable_type,pylint.extensions.overlapping_exceptions,pylint.extensions.docparams,pylint.extensions.mccabe,pylint.extensions.empty_comment [PROJECT_ROOT]
```

black
```cmd
black -l 100 -t py37
```

#### VSCode

```jsonc
{
	// VSCode analysis
	"python.languageServer": "Microsoft",
	"python.analysis.disabled": [
		"unresolved-import"
	],
	"python.linting.maxNumberOfProblems": 200,
	// Bandit
	"python.linting.banditArgs": [
		"-li",
		"--exclude",
		"**/test_*.py",
		"-s",
		"B322",
	],
	"python.linting.banditEnabled": true,
	// Pylint
	"python.linting.pylintUseMinimalCheckers": false,
	"python.linting.pylintArgs": [
		"--disable=pointless-string-statement, superfluous-parens, bad-continuation, wrong-import-position, unsubscriptable-object, python3",
		"--indent-string=\"\t\"",
		"--ignore-patterns=test_.*?py",
		"--argument-naming-style=camelCase",
		"--attr-naming-style=camelCase",
		"--function-naming-style=camelCase",
		"--method-naming-style=camelCase",
		"--variable-naming-style=camelCase",
		"--load-plugins=pylint.extensions.bad_builtin,pylint.extensions.check_elif,pylint.extensions.redefined_variable_type,pylint.extensions.overlapping_exceptions,pylint.extensions.docparams,pylint.extensions.mccabe,pylint.extensions.empty_comment",
	],
	"python.linting.pylintCategorySeverity.convention": "Warning",
	"python.linting.pylintCategorySeverity.refactor": "Warning",
	"python.linting.pylintEnabled": true,
	// Black
	"python.formatting.provider": "black",
	"python.formatting.blackArgs": [
		"-l",
		"100",
		"-t",
		"py37"
	],
}
```
