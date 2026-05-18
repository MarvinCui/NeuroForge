# How To: Logging Config

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test configuring logging using ``logging.config.dictConfig()`` in the Snakefile.

Relevant issue: https://github.com/snakemake/snakemake/issues/3044

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test configuring logging using ``logging.config.dictConfig()`` in the Snakefile.\n\n    Relevant issue: https://github.com/snakemake/snakemake/issues/3044\n    '

```python
'Test configuring logging using ``logging.config.dictConfig()`` in the Snakefile.\n\n    Relevant issue: https://github.com/snakemake/snakemake/issues/3044\n    '
```

**Verification:**
```python
assert p.returncode == 1
```

### Step 2: Assign snakefile = value

```python
snakefile = dpath('logging/test_logging_config') / 'Snakefile'
```

**Verification:**
```python
assert '[TESTLOGGINGCONFIG]' in stdout
```

### Step 3: Assign p = sp.Popen(...)

```python
p = sp.Popen(f'snakemake -s {snakefile}', shell=True, stdout=sp.PIPE, stderr=sp.PIPE, cwd=tmp_path)
```

### Step 4: Assign unknown = p.communicate(...)

```python
stdout, stderr = p.communicate()
```

### Step 5: Assign stdout = stdout.decode(...)

```python
stdout = stdout.decode()
```

**Verification:**
```python
assert p.returncode == 1
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test configuring logging using ``logging.config.dictConfig()`` in the Snakefile.\n\n    Relevant issue: https://github.com/snakemake/snakemake/issues/3044\n    '
snakefile = dpath('logging/test_logging_config') / 'Snakefile'
p = sp.Popen(f'snakemake -s {snakefile}', shell=True, stdout=sp.PIPE, stderr=sp.PIPE, cwd=tmp_path)
stdout, stderr = p.communicate()
stdout = stdout.decode()
assert p.returncode == 1
assert '[TESTLOGGINGCONFIG]' in stdout
```

## Next Steps


---

*Source: test_logging.py:139 | Complexity: Intermediate | Last updated: 2026-05-18*