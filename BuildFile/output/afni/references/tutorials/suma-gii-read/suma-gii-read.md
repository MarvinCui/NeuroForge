# How To: Suma Gii Read

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test suma gii read

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

### Step 1: Assign cmd = "\n    suma -npb {unique_gui_port} -i_gii {data.gii_dset} -drive_com '-com kill_suma'\n    "

```python
cmd = "\n    suma -npb {unique_gui_port} -i_gii {data.gii_dset} -drive_com '-com kill_suma'\n    "
```

**Verification:**
```python
assert not any((pat in stdout for pat in SUMA_FAILURE_PATTERNS))
```

### Step 2: Assign cmd = cmd.format(...)

```python
cmd = cmd.format(**locals())
```

### Step 3: Assign unknown = tools.run_cmd(...)

```python
stdout_log, stderr_log = tools.run_cmd(data, cmd, x_execution_mode=WRAP_SUMA)
```

### Step 4: Assign stdout = stdout_log.read_text(...)

```python
stdout = stdout_log.read_text()
```

**Verification:**
```python
assert not any((pat in stdout for pat in SUMA_FAILURE_PATTERNS))
```


## Complete Example

```python
# Setup
# Fixtures: data, unique_gui_port

# Workflow
cmd = "\n    suma -npb {unique_gui_port} -i_gii {data.gii_dset} -drive_com '-com kill_suma'\n    "
cmd = cmd.format(**locals())
stdout_log, stderr_log = tools.run_cmd(data, cmd, x_execution_mode=WRAP_SUMA)
stdout = stdout_log.read_text()
assert not any((pat in stdout for pat in SUMA_FAILURE_PATTERNS))
```

## Next Steps


---

*Source: test_guis.py:116 | Complexity: Intermediate | Last updated: 2026-05-18*