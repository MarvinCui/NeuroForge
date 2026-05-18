# How To: Afni Gui Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test afni gui basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `afni_test_utils`
- `logging`
- `pathlib`
- `pytest`
- `os`
- `subprocess`
- `unittest.mock`
- `shutil`
- `sys`
- `tempfile`

**Setup Required:**
```python
# Fixtures: data, unique_gui_port
```

## Step-by-Step Guide

### Step 1: Assign outfile = value

```python
outfile = Path(tempfile.mkdtemp()) / 'test'
```

**Verification:**
```python
assert 'Fatal Signal 11' not in stdout
```

### Step 2: Assign cmd = '\n    afni -no_detach -npb {unique_gui_port} -com "OPEN_WINDOW axialimage; SAVE_JPEG axialimage {outfile}; QUIT"\n    '

```python
cmd = '\n    afni -no_detach -npb {unique_gui_port} -com "OPEN_WINDOW axialimage; SAVE_JPEG axialimage {outfile}; QUIT"\n    '
```

**Verification:**
```python
assert 'FATAL ERROR' not in stdout
```

### Step 3: Assign cmd = cmd.format(...)

```python
cmd = cmd.format(**locals())
```

### Step 4: Assign unknown = tools.run_cmd(...)

```python
stdout_log, stderr_log = tools.run_cmd(data, cmd, x_execution_mode='xvfb', timeout=60)
```

### Step 5: Assign stdout = stdout_log.read_text(...)

```python
stdout = stdout_log.read_text()
```

**Verification:**
```python
assert 'Fatal Signal 11' not in stdout
```


## Complete Example

```python
# Setup
# Fixtures: data, unique_gui_port

# Workflow
outfile = Path(tempfile.mkdtemp()) / 'test'
cmd = '\n    afni -no_detach -npb {unique_gui_port} -com "OPEN_WINDOW axialimage; SAVE_JPEG axialimage {outfile}; QUIT"\n    '
cmd = cmd.format(**locals())
stdout_log, stderr_log = tools.run_cmd(data, cmd, x_execution_mode='xvfb', timeout=60)
stdout = stdout_log.read_text()
assert 'Fatal Signal 11' not in stdout
assert 'FATAL ERROR' not in stdout
```

## Next Steps


---

*Source: test_guis.py:63 | Complexity: Intermediate | Last updated: 2026-05-18*