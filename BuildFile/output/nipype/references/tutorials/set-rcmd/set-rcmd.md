# How To: Set Rcmd

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test set rcmd

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `pytest`
- `nipype.interfaces`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign cwd = tmpdir.chdir(...)

```python
cwd = tmpdir.chdir()
```

**Verification:**
```python
assert not os.path.exists(default_script_file), 'scriptfile should not exist.'
```

### Step 2: Assign default_script_file = value

```python
default_script_file = r.RInputSpec().script_file
```

**Verification:**
```python
assert ri._cmd == 'foo'
```

### Step 3: Assign ri = r.RCommand(...)

```python
ri = r.RCommand()
```

### Step 4: Assign _default_r_cmd = value

```python
_default_r_cmd = ri._cmd
```

### Step 5: Call ri.set_default_r_cmd()

```python
ri.set_default_r_cmd('foo')
```

**Verification:**
```python
assert not os.path.exists(default_script_file), 'scriptfile should not exist.'
```

### Step 6: Call ri.set_default_r_cmd()

```python
ri.set_default_r_cmd(_default_r_cmd)
```

### Step 7: Call cwd.chdir()

```python
cwd.chdir()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
cwd = tmpdir.chdir()
default_script_file = r.RInputSpec().script_file
ri = r.RCommand()
_default_r_cmd = ri._cmd
ri.set_default_r_cmd('foo')
assert not os.path.exists(default_script_file), 'scriptfile should not exist.'
assert ri._cmd == 'foo'
ri.set_default_r_cmd(_default_r_cmd)
cwd.chdir()
```

## Next Steps


---

*Source: test_r.py:51 | Complexity: Intermediate | Last updated: 2026-05-18*