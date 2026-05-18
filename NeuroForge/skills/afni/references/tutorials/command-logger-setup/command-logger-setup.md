# How To: Command Logger Setup

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test command logger setup

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `argparse`
- `collections`
- `pathlib`
- `pathlib`
- `unittest.mock`
- `importlib`
- `logging`
- `os`
- `pytest`
- `runpy`
- `shlex`
- `shutil`
- `subprocess`
- `subprocess`
- `signal`
- `sys`
- `tempfile`
- `time`
- `io`
- `contextlib`
- `contextlib`
- `afni_test_utils`
- `afni_test_utils`
- `afni_test_utils`
- `afni_test_utils`
- `afni_test_utils`
- `afni_test_utils.misc`
- `afnipy`
- `afni_test_utils`

**Setup Required:**
```python
# Fixtures: data, monkeypatch
```

## Step-by-Step Guide

### Step 1: Assign logger_in = value

```python
logger_in = data.logger
```

**Verification:**
```python
assert logger_out == logger_in
```

### Step 2: Assign unknown = tools.setup_logging(...)

```python
logger_out, cmd_log, stdout_log, stderr_log = tools.setup_logging(data, logger_in)
```

**Verification:**
```python
assert all((p.parent == data.logdir for p in [cmd_log, stdout_log, stderr_log]))
```

### Step 3: Assign unknown = tools.setup_logging(...)

```python
logger_out, cmd_log, stdout_log, stderr_log = tools.setup_logging(data, None)
```

**Verification:**
```python
assert logger_out == data.logger
```

### Step 4: Assign data.logger = None

```python
data.logger = None
```

**Verification:**
```python
assert all((p.parent == data.logdir for p in [cmd_log, stdout_log, stderr_log]))
```

### Step 5: Assign unknown = tools.setup_logging(...)

```python
logger_out, cmd_log, stdout_log, stderr_log = tools.setup_logging(data, None)
```

**Verification:**
```python
assert logger_out == logging
```


## Complete Example

```python
# Setup
# Fixtures: data, monkeypatch

# Workflow
logger_in = data.logger
logger_out, cmd_log, stdout_log, stderr_log = tools.setup_logging(data, logger_in)
assert logger_out == logger_in
assert all((p.parent == data.logdir for p in [cmd_log, stdout_log, stderr_log]))
logger_out, cmd_log, stdout_log, stderr_log = tools.setup_logging(data, None)
assert logger_out == data.logger
assert all((p.parent == data.logdir for p in [cmd_log, stdout_log, stderr_log]))
data.logger = None
logger_out, cmd_log, stdout_log, stderr_log = tools.setup_logging(data, None)
assert logger_out == logging
assert all((p.parent == data.logdir for p in [cmd_log, stdout_log, stderr_log]))
```

## Next Steps


---

*Source: test_testing_script_functionality.py:227 | Complexity: Intermediate | Last updated: 2026-05-18*