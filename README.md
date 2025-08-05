# Python isort Complete Reference Card

## Overview

`isort` is a Python utility that automatically sorts and organizes import statements in Python files according to PEP 8 guidelines and customizable rules.

## Installation

```bash
pip install isort
```

## Basic Usage

### Command Line

```bash
# Sort imports in a single file
isort myfile.py

# Sort imports in multiple files
isort file1.py file2.py file3.py

# Sort all Python files in current directory
isort *.py

# Sort all Python files recursively
isort .

# Check what changes would be made (dry run)
isort --check-only myfile.py

# Show diff of changes
isort --diff myfile.py

# Force single line imports
isort --force-single-line myfile.py
```

### Python API

```python
import isort

# Sort a file
isort.file("myfile.py")

# Sort code string
sorted_code = isort.code("import os\nimport sys")

# Check if file is sorted
is_sorted = isort.check_file("myfile.py")
```

## Import Categories (Default Order)

1. **Standard Library** - Built-in Python modules
1. **Third Party** - Installed packages
1. **Local/First Party** - Your project modules

### Example of Sorted Imports

```python
# Standard library imports
import os
import sys
from pathlib import Path

# Third-party imports
import numpy as np
import pandas as pd
import requests

# Local application imports
from myapp import config
from myapp.models import User
```

## Configuration Methods

### 1. Command Line Arguments

```bash
isort --profile=black --line-length=88 myfile.py
```

### 2. Configuration File (.isort.cfg)

```ini
[settings]
profile = black
line_length = 88
multi_line_output = 3
include_trailing_comma = true
force_grid_wrap = 0
use_parentheses = true
ensure_newline_before_comments = true
```

### 3. pyproject.toml

```toml
[tool.isort]
profile = "black"
line_length = 88
multi_line_output = 3
include_trailing_comma = true
force_grid_wrap = 0
use_parentheses = true
ensure_newline_before_comments = true
```

### 4. setup.cfg

```ini
[isort]
profile = black
line_length = 88
multi_line_output = 3
```

## Complete Command Line Options Table

|Option                        |Short|Description                                  |Example                             |
|------------------------------|-----|---------------------------------------------|------------------------------------|
|`--help`                      |`-h` |Show help message                            |`isort -h`                          |
|`--check-only`                |`-c` |Check if imports are sorted without modifying|`isort -c myfile.py`                |
|`--diff`                      |`-d` |Show diff of changes                         |`isort -d myfile.py`                |
|`--interactive`               |     |Interactive mode for conflict resolution     |`isort --interactive`               |
|`--apply`                     |     |Apply changes (opposite of check-only)       |`isort --apply`                     |
|`--recursive`                 |`-r` |Recursively sort directories                 |`isort -r .`                        |
|`--quiet`                     |`-q` |Suppress output                              |`isort -q myfile.py`                |
|`--verbose`                   |`-v` |Verbose output                               |`isort -v myfile.py`                |
|`--stdout`                    |     |Print to stdout instead of modifying file    |`isort --stdout myfile.py`          |
|`--overwrite-in-place`        |     |Overwrite file in place                      |`isort --overwrite-in-place`        |
|`--show-files`                |     |Show files that would be sorted              |`isort --show-files .`              |
|`--skip`                      |`-s` |Skip files/directories                       |`isort -s __init__.py`              |
|`--extend-skip`               |     |Extend default skip list                     |`isort --extend-skip=migrations`    |
|`--skip-glob`                 |     |Skip files matching glob pattern             |`isort --skip-glob=*_pb2.py`        |
|`--filter-files`              |     |Filter files to sort                         |`isort --filter-files`              |
|`--profile`                   |     |Use predefined profile                       |`isort --profile=black`             |
|`--force-single-line`         |`-sl`|Force single line imports                    |`isort -sl`                         |
|`--line-length`               |`-l` |Set line length                              |`isort -l 100`                      |
|`--wrap-length`               |`-w` |Set wrap length                              |`isort -w 88`                       |
|`--multi-line`                |`-m` |Multi-line output mode (0-5)                 |`isort -m 3`                        |
|`--trailing-comma`            |`-tc`|Include trailing comma                       |`isort -tc`                         |
|`--force-grid-wrap`           |     |Force grid wrap at specified length          |`isort --force-grid-wrap=2`         |
|`--use-parentheses`           |     |Use parentheses for line continuation        |`isort --use-parentheses`           |
|`--combine-as`                |     |Combine as imports                           |`isort --combine-as`                |
|`--combine-star`              |     |Combine star imports                         |`isort --combine-star`              |
|`--force-sort-within-sections`|     |Force sorting within sections                |`isort --force-sort-within-sections`|
|`--case-sensitive`            |     |Case sensitive sorting                       |`isort --case-sensitive`            |
|`--remove-redundant-aliases`  |     |Remove redundant aliases                     |`isort --remove-redundant-aliases`  |
|`--honor-noqa`                |     |Honor # noqa comments                        |`isort --honor-noqa`                |

## Multi-line Output Modes

|Mode|Description     |Example                                                            |
|----|----------------|-------------------------------------------------------------------|
|0   |Grid            |`from third_party import (alpha, bravo, charlie)`                  |
|1   |Vertical        |`from third_party import (alpha,\n    bravo,\n    charlie)`        |
|2   |Hanging indent  |`from third_party import alpha,\\\n    bravo, charlie`             |
|3   |Vertical hanging|`from third_party import (\n    alpha,\n    bravo,\n    charlie\n)`|
|4   |Hanging grid    |`from third_party import (\n    alpha, bravo,\n    charlie\n)`     |
|5   |No indent       |`from third_party import (\nalpha,\nbravo,\ncharlie\n)`            |

## Built-in Profiles

|Profile     |Description                    |Compatible With  |
|------------|-------------------------------|-----------------|
|`black`     |Compatible with Black formatter|Black            |
|`django`    |Django coding style            |Django projects  |
|`pycharm`   |PyCharm default settings       |PyCharm IDE      |
|`google`    |Google Python style guide      |Google style     |
|`open_stack`|OpenStack style guide          |OpenStack        |
|`plone`     |Plone coding style             |Plone CMS        |
|`attrs`     |attrs library style            |attrs library    |
|`hug`       |hug framework style            |hug API framework|

## Advanced Configuration Options

### Custom Import Sections

```toml
[tool.isort]
known_first_party = ["myapp", "mypackage"]
known_third_party = ["django", "requests", "numpy"]
known_local_folder = ["local_package"]
sections = ["FUTURE", "STDLIB", "THIRDPARTY", "FIRSTPARTY", "LOCALFOLDER"]
```

### Import Length and Wrapping

```toml
[tool.isort]
line_length = 88
wrap_length = 88
multi_line_output = 3
include_trailing_comma = true
force_grid_wrap = 0
use_parentheses = true
```

### Sorting Behavior

```toml
[tool.isort]
force_sort_within_sections = true
lexicographical = true
case_sensitive = false
reverse_relative = false
group_by_package = false
```

### Skip Patterns

```toml
[tool.isort]
skip = ["__init__.py", "migrations"]
skip_glob = ["**/migrations/*", "**/*_pb2.py"]
extend_skip = ["setup.py"]
```

## Code Examples

### Before isort

```python
import sys
from myapp.models import User
import os
from django.db import models
import requests
from pathlib import Path
from myapp import settings
import numpy as np
```

### After isort (default)

```python
import os
import sys
from pathlib import Path

import numpy as np
import requests
from django.db import models

from myapp import settings
from myapp.models import User
```

### With Black Profile

```python
import os
import sys
from pathlib import Path

import numpy as np
import requests
from django.db import models

from myapp import settings
from myapp.models import User
```

## Special Comments and Annotations

### Skip Import Sorting

```python
# isort:skip_file
import unsorted
import imports
```

### Skip Individual Imports

```python
import normally_sorted  # isort:skip
import also_normally_sorted
```

### Split Imports

```python
from __future__ import annotations  # isort:split
import standard_library
```

## Integration Examples

### Pre-commit Hook

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/pycqa/isort
    rev: 5.12.0
    hooks:
      - id: isort
        args: ["--profile", "black", "--filter-files"]
```

### GitHub Actions

```yaml
- name: Check import sorting
  run: |
    pip install isort
    isort --check-only --diff .
```

### Makefile Integration

```makefile
.PHONY: format
format:
	isort .
	black .

.PHONY: lint
lint:
	isort --check-only --diff .
	black --check .
```

## Python API Reference

### Core Functions

```python
import isort

# Sort file in place
isort.file("myfile.py")

# Sort code string and return result
sorted_code = isort.code("import os\nimport sys")

# Check if file/code is sorted
is_sorted = isort.check_file("myfile.py")
is_code_sorted = isort.check_code_string("import sys\nimport os")

# Get differences
diff = isort.diff.diff_code_string("import sys\nimport os")

# Stream processing
import io
input_stream = io.StringIO("import sys\nimport os")
output_stream = io.StringIO()
isort.stream(input_stream, output_stream)
```

### Custom Configuration

```python
from isort import Config, api

# Create custom config
config = Config(
    profile="black",
    line_length=100,
    multi_line_output=3,
    known_first_party=["myapp"]
)

# Use with API
sorted_code = api.sort_code_string(
    "import os\nfrom myapp import models", 
    config=config
)
```

## Troubleshooting

### Common Issues

1. **Import not recognized as first-party**
   
   ```toml
   [tool.isort]
   known_first_party = ["your_package_name"]
   ```
1. **Conflicts with Black formatter**
   
   ```toml
   [tool.isort]
   profile = "black"
   ```
1. **Skip problematic files**
   
   ```toml
   [tool.isort]
   skip_glob = ["**/migrations/*", "venv/*"]
   ```
1. **Performance on large codebases**
   
   ```bash
   isort --jobs=4 .  # Use multiple processes
   ```

### Debugging

```bash
# Verbose output to see what isort is doing
isort --verbose --diff myfile.py

# Show all files that would be processed
isort --show-files .

# Check current settings
isort --show-diff --settings-path .
```

## Best Practices

1. **Use profiles** for consistency with other tools
1. **Configure in pyproject.toml** for modern Python projects
1. **Add to pre-commit hooks** for automatic enforcement
1. **Test with –check-only** in CI/CD pipelines
1. **Use –diff** to review changes before applying
1. **Combine with Black** using the black profile
1. **Set known_first_party** for accurate categorization
1. **Use skip patterns** for generated or vendored code

## Performance Tips

- Use `--filter-files` to process only Python files
- Skip unnecessary directories with `--skip` or `--skip-glob`
- Use `--jobs` for parallel processing on large codebases
- Consider `--atomic` for safer file operations