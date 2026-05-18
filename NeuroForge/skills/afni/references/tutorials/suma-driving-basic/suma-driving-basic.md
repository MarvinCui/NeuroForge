# How To: Suma Driving Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test suma driving basic

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

### Step 1: Assign cmd = '\n    export SUMA_DriveSumaMaxWait=5;\n    suma -niml -npb {unique_gui_port} &     echo suma started;\n    sleep 6;\n    echo recording image;\n    DriveSuma -npb {unique_gui_port} -com viewer_cont -key \'Ctrl+r\';\n    DriveSuma -npb {unique_gui_port} -com \'kill_suma\';\n    echo image recorded;\n    echo "++ Done";\n    '

```python
cmd = '\n    export SUMA_DriveSumaMaxWait=5;\n    suma -niml -npb {unique_gui_port} &     echo suma started;\n    sleep 6;\n    echo recording image;\n    DriveSuma -npb {unique_gui_port} -com viewer_cont -key \'Ctrl+r\';\n    DriveSuma -npb {unique_gui_port} -com \'kill_suma\';\n    echo image recorded;\n    echo "++ Done";\n    '
```

**Verification:**
```python
assert not any((pat in stdout for pat in SUMA_FAILURE_PATTERNS))
```

### Step 2: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, merge_error_with_output=True, skip_output_diff=True)
```

### Step 3: Assign unknown = differ.run(...)

```python
stdout_log, stderr_log = differ.run(x_execution_mode=WRAP_SUMA, workdir=data.outdir)
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
cmd = '\n    export SUMA_DriveSumaMaxWait=5;\n    suma -niml -npb {unique_gui_port} &     echo suma started;\n    sleep 6;\n    echo recording image;\n    DriveSuma -npb {unique_gui_port} -com viewer_cont -key \'Ctrl+r\';\n    DriveSuma -npb {unique_gui_port} -com \'kill_suma\';\n    echo image recorded;\n    echo "++ Done";\n    '
differ = tools.OutputDiffer(data, cmd, merge_error_with_output=True, skip_output_diff=True)
stdout_log, stderr_log = differ.run(x_execution_mode=WRAP_SUMA, workdir=data.outdir)
stdout = stdout_log.read_text()
assert not any((pat in stdout for pat in SUMA_FAILURE_PATTERNS))
```

## Next Steps


---

*Source: test_guis.py:137 | Complexity: Intermediate | Last updated: 2026-05-18*