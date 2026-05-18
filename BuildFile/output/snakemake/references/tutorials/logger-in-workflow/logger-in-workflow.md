# How To: Logger In Workflow

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test adding a handler to the ``logger`` global in the Snakefile.

relevant issue: https://github.com/snakemake/snakemake/issues/3558

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

### Step 1: 'Test adding a handler to the ``logger`` global in the Snakefile.\n\n    relevant issue: https://github.com/snakemake/snakemake/issues/3558\n    '

```python
'Test adding a handler to the ``logger`` global in the Snakefile.\n\n    relevant issue: https://github.com/snakemake/snakemake/issues/3558\n    '
```

**Verification:**
```python
assert os.path.exists(log_dir), f'Log directory {log_dir} not found'
```

### Step 2: Assign tmpdir = run(...)

```python
tmpdir = run(dpath('logging/test_workflow_logger'), cleanup=False, check_results=False)
```

**Verification:**
```python
assert log_files, 'No log files found'
```

### Step 3: Assign stmts = value

```python
stmts = ['TESTINFO', 'TESTWARN', 'TESTERROR']
```

**Verification:**
```python
assert stmt.strip() in log_content.strip(), f'Expected statement {stmt} not found in log file. Log content: {log_content}'
```

### Step 4: Assign log_dir = os.path.join(...)

```python
log_dir = os.path.join(tmpdir, '.snakemake', 'log')
```

**Verification:**
```python
assert stmt.strip() in custom_log_content.strip(), f'Expected statement {stmt} not found in log file. Custom Log content: {custom_log_content}'
```

### Step 5: Assign log_files = glob.glob(...)

```python
log_files = glob.glob(os.path.join(log_dir, '*.snakemake.log'))
```

**Verification:**
```python
assert log_files, 'No log files found'
```

### Step 6: Call log_files.sort()

```python
log_files.sort(key=os.path.getmtime, reverse=True)
```

### Step 7: Assign latest_log = value

```python
latest_log = log_files[0]
```

### Step 8: Assign custom_log = os.path.join(...)

```python
custom_log = os.path.join(tmpdir, 'mylog.txt')
```

### Step 9: Call shutil.rmtree()

```python
shutil.rmtree(tmpdir, ignore_errors=ON_WINDOWS)
```

### Step 10: Assign log_content = f.read(...)

```python
log_content = f.read()
```

### Step 11: Assign custom_log_content = f.read(...)

```python
custom_log_content = f.read()
```

**Verification:**
```python
assert stmt.strip() in log_content.strip(), f'Expected statement {stmt} not found in log file. Log content: {log_content}'
```


## Complete Example

```python
# Workflow
'Test adding a handler to the ``logger`` global in the Snakefile.\n\n    relevant issue: https://github.com/snakemake/snakemake/issues/3558\n    '
import glob
tmpdir = run(dpath('logging/test_workflow_logger'), cleanup=False, check_results=False)
stmts = ['TESTINFO', 'TESTWARN', 'TESTERROR']
log_dir = os.path.join(tmpdir, '.snakemake', 'log')
assert os.path.exists(log_dir), f'Log directory {log_dir} not found'
log_files = glob.glob(os.path.join(log_dir, '*.snakemake.log'))
assert log_files, 'No log files found'
log_files.sort(key=os.path.getmtime, reverse=True)
latest_log = log_files[0]
with open(latest_log, 'r') as f:
    log_content = f.read()
custom_log = os.path.join(tmpdir, 'mylog.txt')
with open(custom_log, 'r') as f:
    custom_log_content = f.read()
for stmt in stmts:
    assert stmt.strip() in log_content.strip(), f'Expected statement {stmt} not found in log file. Log content: {log_content}'
    assert stmt.strip() in custom_log_content.strip(), f'Expected statement {stmt} not found in log file. Custom Log content: {custom_log_content}'
shutil.rmtree(tmpdir, ignore_errors=ON_WINDOWS)
```

## Next Steps


---

*Source: test_logging.py:159 | Complexity: Advanced | Last updated: 2026-05-18*