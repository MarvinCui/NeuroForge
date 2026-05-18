# How To: Run Interface

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test run interface

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
assert not os.path.exists(default_script_file), 'scriptfile should not exist 1.'
```

### Step 2: Assign default_script_file = value

```python
default_script_file = r.RInputSpec().script_file
```

**Verification:**
```python
assert not os.path.exists(default_script_file), 'scriptfile should not exist 2.'
```

### Step 3: Assign rc = r.RCommand(...)

```python
rc = r.RCommand(r_cmd='foo_m')
```

**Verification:**
```python
assert not os.path.exists(default_script_file), 'scriptfile should not exist 3.'
```

### Step 4: Assign rc.inputs.script = 'a=1;'

```python
rc.inputs.script = 'a=1;'
```

**Verification:**
```python
assert os.path.exists(default_script_file), 'scriptfile should exist 3.'
```

### Step 5: Call cwd.chdir()

```python
cwd.chdir()
```

### Step 6: Call rc.run()

```python
rc.run()
```

### Step 7: Call os.remove()

```python
os.remove(default_script_file)
```

### Step 8: Call rc.run()

```python
rc.run()
```

### Step 9: Call os.remove()

```python
os.remove(default_script_file)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
cwd = tmpdir.chdir()
default_script_file = r.RInputSpec().script_file
rc = r.RCommand(r_cmd='foo_m')
assert not os.path.exists(default_script_file), 'scriptfile should not exist 1.'
with pytest.raises(ValueError):
    rc.run()
assert not os.path.exists(default_script_file), 'scriptfile should not exist 2.'
if os.path.exists(default_script_file):
    os.remove(default_script_file)
rc.inputs.script = 'a=1;'
assert not os.path.exists(default_script_file), 'scriptfile should not exist 3.'
with pytest.raises(IOError):
    rc.run()
assert os.path.exists(default_script_file), 'scriptfile should exist 3.'
if os.path.exists(default_script_file):
    os.remove(default_script_file)
cwd.chdir()
```

## Next Steps


---

*Source: test_r.py:28 | Complexity: Advanced | Last updated: 2026-05-18*