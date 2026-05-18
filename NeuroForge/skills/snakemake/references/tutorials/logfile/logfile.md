# How To: Logfile

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logfile

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

### Step 1: Assign tmpdir = run(...)

```python
tmpdir = run(dpath('logging/test_logfile'), cleanup=False, check_results=False)
```

**Verification:**
```python
assert os.path.exists(log_dir), f'Log directory {log_dir} not found'
```

### Step 2: Assign finished_stmt = '\nFinished jobid: 0 (Rule: all)\n6 of 6 steps (100%) done'

```python
finished_stmt = '\nFinished jobid: 0 (Rule: all)\n6 of 6 steps (100%) done'
```

**Verification:**
```python
assert log_files, 'No log files found'
```

### Step 3: Assign log_dir = os.path.join(...)

```python
log_dir = os.path.join(tmpdir, '.snakemake', 'log')
```

**Verification:**
```python
assert finished_stmt.strip() in log_content.strip(), f'Expected statement not found in log file. Log content: {log_content}'
```

### Step 4: Assign log_files = glob.glob(...)

```python
log_files = glob.glob(os.path.join(log_dir, '*.snakemake.log'))
```

**Verification:**
```python
assert log_files, 'No log files found'
```

### Step 5: Call log_files.sort()

```python
log_files.sort(key=os.path.getmtime, reverse=True)
```

### Step 6: Assign latest_log = value

```python
latest_log = log_files[0]
```

**Verification:**
```python
assert finished_stmt.strip() in log_content.strip(), f'Expected statement not found in log file. Log content: {log_content}'
```

### Step 7: Call shutil.rmtree()

```python
shutil.rmtree(tmpdir, ignore_errors=ON_WINDOWS)
```

### Step 8: Assign log_content = f.read(...)

```python
log_content = f.read()
```


## Complete Example

```python
# Workflow
import glob
tmpdir = run(dpath('logging/test_logfile'), cleanup=False, check_results=False)
finished_stmt = '\nFinished jobid: 0 (Rule: all)\n6 of 6 steps (100%) done'
log_dir = os.path.join(tmpdir, '.snakemake', 'log')
assert os.path.exists(log_dir), f'Log directory {log_dir} not found'
log_files = glob.glob(os.path.join(log_dir, '*.snakemake.log'))
assert log_files, 'No log files found'
log_files.sort(key=os.path.getmtime, reverse=True)
latest_log = log_files[0]
with open(latest_log, 'r') as f:
    log_content = f.read()
assert finished_stmt.strip() in log_content.strip(), f'Expected statement not found in log file. Log content: {log_content}'
shutil.rmtree(tmpdir, ignore_errors=ON_WINDOWS)
```

## Next Steps


---

*Source: test_logging.py:79 | Complexity: Advanced | Last updated: 2026-05-18*