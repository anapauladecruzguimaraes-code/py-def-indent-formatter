# py-def-indent-formatter

A command line tool (and a pre-commit hook) to automatically format haning indentation in Python function definitions to 8 spaces.

Currently, this tool is only designed to work properly _after_ your Python files have been formatted by [`black`](https://github.com/psf/black) or [`blue`](https://github.com/grantjenks/blue).

## Motivation of this tool

`black` and `blue` both use only 4 spaces as haning indentation in function definitions, which is not aligned with [PEP8's recommendation](https://peps.python.org/pep-0008/#indentation).

Therefore, this tool specifically fixes this 4-space style choice of `black` and `blue`.

## Installation

```bash
pip install format-def-indent
```

## Usage

### As a command line tool

To auto-format Python files (.py):

```bash
format-def-indent <PATH_THAT_CONTAINS_PYTHON_FILES>
```
Use `--help` to see documentations of command line arguments.

To auto-format Jupyter notebooks (.ipynb):

```bash
format-def-indent-in-jupyter <PATH_THAT_CONTAINS_PYTHON_FILES>
```

### As a pre-commit hook

To auto-format Python files (.py), put the following into your `.pre-commit-config.yaml` file. Remember to replace `<VERSION>` with your version of this tool (such as `v0.1.4`):
```yaml
-   repo: https://github.com/cyyc1/py-def-indent-formatter
    rev: <VERSION>
    hooks:
    -   id: format-def-indent
```

To auto-format Jupyter notebooks (.ipynb), put the following into your `.pre-commit-config.yaml` file:
```yaml
-   repo: https://github.com/cyyc1/py-def-indent-formatter
    rev: <VERSION>
    hooks:
    -   id: format-def-indent-in-jupyter
```

See [pre-commit](https://github.com/pre-commit/pre-commit) for more instructions.

## What does this formatter do

This tool formats the following "before" (red) into "after" (green).

### Multi-line arguments in function definitions:

```diff
def some_function(
+    arg1,
+    arg2='test',
+    *,
+    arg3: int = 2,
+    arg4: bool = False,
+        arg1,
+        arg2='test',
+        *,
+        arg3: int = 2,
+        arg4: bool = False,
) -> None:
    print(1)
```

or

```diff
def some_functions(
-    arg1,
-    *args,
-    **kwargs,
+        arg1,
+        *args,
+        **kwargs,
):
    print(1)
```

### Single-line arguments in function definitions:

```diff
def some_function(
-    arg1, arg2='test', *, arg3: int = 2, arg4: bool = False,
+        arg1, arg2='test', *, arg3: int = 2, arg4: bool = False,
):
    print(1)
```
