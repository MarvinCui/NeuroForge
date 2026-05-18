# How To: Execute Cmd Args

**Difficulty**: Advanced
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test execute cmd args

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
# Fixtures: params
```

## Step-by-Step Guide

### Step 1: Assign tmpdir = Path(...)

```python
tmpdir = Path(tempfile.gettempdir())
```

**Verification:**
```python
assert timed_out == params['expected_to_timeout']
```

### Step 2: Assign stdout = value

```python
stdout = tmpdir / 'text.txt'
```

### Step 3: Assign stderr = value

```python
stderr = tmpdir / 'other_text.txt'
```

**Verification:**
```python
assert timed_out == params['expected_to_timeout']
```

### Step 4: Assign proc = tools.__execute_cmd_args(...)

```python
proc = tools.__execute_cmd_args(params['cmd_args'], logging, stdout, stderr, tmpdir, timeout=params['timeout'])
```

### Step 5: Assign timed_out = False

```python
timed_out = False
```

### Step 6: Assign timed_out = True

```python
timed_out = True
```


## Complete Example

```python
# Setup
# Fixtures: params

# Workflow
tmpdir = Path(tempfile.gettempdir())
stdout = tmpdir / 'text.txt'
stderr = tmpdir / 'other_text.txt'
try:
    proc = tools.__execute_cmd_args(params['cmd_args'], logging, stdout, stderr, tmpdir, timeout=params['timeout'])
    timed_out = False
except (TimeoutError, subprocess.TimeoutExpired):
    timed_out = True
assert timed_out == params['expected_to_timeout']
```

## Next Steps


---

*Source: test_testing_script_functionality.py:151 | Complexity: Advanced | Last updated: 2026-05-18*