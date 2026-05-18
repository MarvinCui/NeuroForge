# How To: No Mod Cmd Var Works

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test no mod cmd var works

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
# Fixtures: monkeypatch, data
```

## Step-by-Step Guide

### Step 1: Assign cmd = value

```python
cmd = f"{' '.join([str(data.outdir) for x in range(5)])} "
```

**Verification:**
```python
assert com.com == com.trimcom
```

### Step 2: Call monkeypatch.setenv()

```python
monkeypatch.setenv('NO_CMD_MOD', 'True')
```

**Verification:**
```python
assert com.com != com.trimcom
```

### Step 3: Assign com = afnipy.afni_base.shell_com(...)

```python
com = afnipy.afni_base.shell_com(cmd)
```

**Verification:**
```python
assert com.com != com.trimcom
```

### Step 4: Call monkeypatch.setenv()

```python
monkeypatch.setenv('NO_CMD_MOD', 'no')
```

### Step 5: Assign com = afnipy.afni_base.shell_com(...)

```python
com = afnipy.afni_base.shell_com(cmd)
```

**Verification:**
```python
assert com.com != com.trimcom
```

### Step 6: Call monkeypatch.delenv()

```python
monkeypatch.delenv('NO_CMD_MOD')
```

### Step 7: Assign com = afnipy.afni_base.shell_com(...)

```python
com = afnipy.afni_base.shell_com(cmd)
```

**Verification:**
```python
assert com.com != com.trimcom
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch, data

# Workflow
cmd = f"{' '.join([str(data.outdir) for x in range(5)])} "
monkeypatch.setenv('NO_CMD_MOD', 'True')
com = afnipy.afni_base.shell_com(cmd)
assert com.com == com.trimcom
monkeypatch.setenv('NO_CMD_MOD', 'no')
com = afnipy.afni_base.shell_com(cmd)
assert com.com != com.trimcom
monkeypatch.delenv('NO_CMD_MOD')
com = afnipy.afni_base.shell_com(cmd)
assert com.com != com.trimcom
```

## Next Steps


---

*Source: test_testing_script_functionality.py:1496 | Complexity: Intermediate | Last updated: 2026-05-18*