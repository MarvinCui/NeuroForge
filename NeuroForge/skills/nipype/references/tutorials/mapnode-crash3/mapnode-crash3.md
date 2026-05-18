# How To: Mapnode Crash3

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test mapnode crash when mapnode is embedded in a workflow

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

### Step 1: 'Test mapnode crash when mapnode is embedded in a workflow'

```python
'Test mapnode crash when mapnode is embedded in a workflow'
```

### Step 2: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 3: Assign node = pe.MapNode(...)

```python
node = pe.MapNode(niu.Function(input_names=['WRONG'], output_names=['newstring'], function=dummy_func), iterfield=['WRONG'], name='myfunc')
```

### Step 4: Assign node.inputs.WRONG = value

```python
node.inputs.WRONG = [f'string{i}' for i in range(3)]
```

### Step 5: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow('testmapnodecrash')
```

### Step 6: Call wf.add_nodes()

```python
wf.add_nodes([node])
```

### Step 7: Assign wf.base_dir = value

```python
wf.base_dir = tmpdir.strpath
```

### Step 8: Assign unknown = os.getcwd(...)

```python
wf.config['execution']['crashdump_dir'] = os.getcwd()
```

### Step 9: Call wf.run()

```python
wf.run(plugin='Linear')
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test mapnode crash when mapnode is embedded in a workflow'
tmpdir.chdir()
node = pe.MapNode(niu.Function(input_names=['WRONG'], output_names=['newstring'], function=dummy_func), iterfield=['WRONG'], name='myfunc')
node.inputs.WRONG = [f'string{i}' for i in range(3)]
wf = pe.Workflow('testmapnodecrash')
wf.add_nodes([node])
wf.base_dir = tmpdir.strpath
wf.config['execution']['crashdump_dir'] = os.getcwd()
with pytest.raises(RuntimeError):
    wf.run(plugin='Linear')
```

## Next Steps


---

*Source: test_utils.py:208 | Complexity: Advanced | Last updated: 2026-05-18*