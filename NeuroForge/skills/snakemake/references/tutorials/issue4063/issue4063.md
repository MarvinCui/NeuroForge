# How To: Issue4063

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test issue4063

## Prerequisites

**Required Modules:**
- `os`
- `shutil`
- `sys`
- `subprocess`
- `logging`
- `logging.handlers`
- `collections`
- `pathlib`
- `queue`
- `json`
- `pytest`
- `snakemake_interface_logger_plugins.common`
- `common`
- `conftest`
- `glob`
- `snakemake.logging`
- `snakemake.logging`
- `snakemake.logging`
- `glob`
- `snakemake.logging`
- `snakemake.settings.types`


## Step-by-Step Guide

### Step 1: Assign handler = ColorizingTextHandler(...)

```python
handler = ColorizingTextHandler(stream=sys.stdout)
```

### Step 2: Assign formatter = DefaultFormatter(...)

```python
formatter = DefaultFormatter(quiet=set(), show_failed_logs=False)
```

### Step 3: Call handler.setFormatter()

```python
handler.setFormatter(formatter)
```

### Step 4: Assign log_filter = DefaultFilter(...)

```python
log_filter = DefaultFilter(quiet=set(), debug_dag=False, dryrun=False, printshellcmds=True)
```

### Step 5: Call handler.addFilter()

```python
handler.addFilter(log_filter)
```

### Step 6: Assign handler.handleError = handle_logging_error

```python
handler.handleError = handle_logging_error
```

### Step 7: Assign test_logger = logging.getLogger(...)

```python
test_logger = logging.getLogger('foo')
```

### Step 8: Call test_logger.setLevel()

```python
test_logger.setLevel(logging.INFO)
```

### Step 9: Call test_logger.addHandler()

```python
test_logger.addHandler(handler)
```

### Step 10: Call test_logger.info()

```python
test_logger.info(None, extra={'event': LogEvent.SHELLCMD, 'cmd': "echo 'bar'"})
```

### Step 11: Call test_logger.removeHandler()

```python
test_logger.removeHandler(handler)
```


## Complete Example

```python
# Workflow
from snakemake.logging import ColorizingTextHandler
from snakemake.logging import DefaultFormatter
from snakemake.logging import DefaultFilter
handler = ColorizingTextHandler(stream=sys.stdout)
formatter = DefaultFormatter(quiet=set(), show_failed_logs=False)
handler.setFormatter(formatter)
log_filter = DefaultFilter(quiet=set(), debug_dag=False, dryrun=False, printshellcmds=True)
handler.addFilter(log_filter)

def handle_logging_error(record):
    raise sys.exc_info()[1]
handler.handleError = handle_logging_error
test_logger = logging.getLogger('foo')
test_logger.setLevel(logging.INFO)
test_logger.addHandler(handler)
test_logger.info(None, extra={'event': LogEvent.SHELLCMD, 'cmd': "echo 'bar'"})
test_logger.removeHandler(handler)
```

## Next Steps


---

*Source: test_logging.py:106 | Complexity: Advanced | Last updated: 2026-05-18*