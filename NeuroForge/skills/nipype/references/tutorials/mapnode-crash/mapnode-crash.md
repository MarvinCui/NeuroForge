# How To: Mapnode Crash

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test mapnode crash when stop_on_first_crash is True

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

### Step 1: 'Test mapnode crash when stop_on_first_crash is True'

```python
'Test mapnode crash when stop_on_first_crash is True'
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

### Step 5: Assign node.config = deepcopy(...)

```python
node.config = deepcopy(config._sections)
```

### Step 6: Assign unknown = True

```python
node.config['execution']['stop_on_first_crash'] = True
```

### Step 7: Assign node.base_dir = value

```python
node.base_dir = tmpdir.strpath
```

### Step 8: Call os.chdir()

```python
os.chdir(cwd)
```

### Step 9: Call node.run()

```python
node.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test mapnode crash when stop_on_first_crash is True'
cwd = os.getcwd()
node = pe.MapNode(niu.Function(input_names=['WRONG'], output_names=['newstring'], function=dummy_func), iterfield=['WRONG'], name='myfunc')
node.inputs.WRONG = [f'string{i}' for i in range(3)]
node.config = deepcopy(config._sections)
node.config['execution']['stop_on_first_crash'] = True
node.base_dir = tmpdir.strpath
with pytest.raises(pe.nodes.NodeExecutionError):
    node.run()
os.chdir(cwd)
```

## Next Steps


---

*Source: test_utils.py:171 | Complexity: Advanced | Last updated: 2026-05-18*