# How To: Mapnode Crash2

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test mapnode crash when stop_on_first_crash is False

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `interfaces`
- `interfaces`
- `utils`
- `shutil`
- `numpy`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: 'Test mapnode crash when stop_on_first_crash is False'

```python
'Test mapnode crash when stop_on_first_crash is False'
```

### Step 2: Assign cwd = os.getcwd(...)

```python
cwd = os.getcwd()
```

### Step 3: Assign node = pe.MapNode(...)

```python
node = pe.MapNode(niu.Function(input_names=['WRONG'], output_names=['newstring'], function=dummy_func), iterfield=['WRONG'], name='myfunc')
```

### Step 4: Assign node.inputs.WRONG = value

```python
node.inputs.WRONG = [f'string{i}' for i in range(3)]
```

### Step 5: Assign node.base_dir = value

```python
node.base_dir = tmpdir.strpath
```

### Step 6: Call os.chdir()

```python
os.chdir(cwd)
```

### Step 7: Call node.run()

```python
node.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test mapnode crash when stop_on_first_crash is False'
cwd = os.getcwd()
node = pe.MapNode(niu.Function(input_names=['WRONG'], output_names=['newstring'], function=dummy_func), iterfield=['WRONG'], name='myfunc')
node.inputs.WRONG = [f'string{i}' for i in range(3)]
node.base_dir = tmpdir.strpath
with pytest.raises(Exception):
    node.run()
os.chdir(cwd)
```

## Next Steps


---

*Source: test_utils.py:190 | Complexity: Intermediate | Last updated: 2026-05-18*