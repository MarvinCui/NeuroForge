# How To: Duplicate Node Check

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test duplicate node check

## Prerequisites

**Required Modules:**
- `glob`
- `os`
- `shutil`
- `itertools`
- `pytest`
- `networkx`
- `interfaces`
- `test_base`
- `test_utils`
- `os`
- `os`


## Step-by-Step Guide

### Step 1: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='testidentity')
```

**Verification:**
```python
assert 'Duplicate node name "selector3" found.' == str(excinfo.value)
```

### Step 2: Assign original_list = value

```python
original_list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Step 3: Assign selector1 = pe.Node(...)

```python
selector1 = pe.Node(niu.Select(), name='selector1')
```

### Step 4: Assign selector1.inputs.index = value

```python
selector1.inputs.index = original_list[:-1]
```

### Step 5: Assign selector1.inputs.inlist = original_list

```python
selector1.inputs.inlist = original_list
```

### Step 6: Assign selector2 = pe.Node(...)

```python
selector2 = pe.Node(niu.Select(), name='selector2')
```

### Step 7: Assign selector2.inputs.index = value

```python
selector2.inputs.index = original_list[:-2]
```

### Step 8: Assign selector3 = pe.Node(...)

```python
selector3 = pe.Node(niu.Select(), name='selector3')
```

### Step 9: Assign selector3.inputs.index = value

```python
selector3.inputs.index = original_list[:-3]
```

### Step 10: Assign selector4 = pe.Node(...)

```python
selector4 = pe.Node(niu.Select(), name='selector3')
```

### Step 11: Assign selector4.inputs.index = value

```python
selector4.inputs.index = original_list[:-4]
```

### Step 12: Assign wf_connections = value

```python
wf_connections = [(selector1, selector2, [('out', 'inlist')]), (selector2, selector3, [('out', 'inlist')]), (selector3, selector4, [('out', 'inlist')])]
```

**Verification:**
```python
assert 'Duplicate node name "selector3" found.' == str(excinfo.value)
```

### Step 13: Call wf.connect()

```python
wf.connect(wf_connections)
```


## Complete Example

```python
# Workflow
wf = pe.Workflow(name='testidentity')
original_list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
selector1 = pe.Node(niu.Select(), name='selector1')
selector1.inputs.index = original_list[:-1]
selector1.inputs.inlist = original_list
selector2 = pe.Node(niu.Select(), name='selector2')
selector2.inputs.index = original_list[:-2]
selector3 = pe.Node(niu.Select(), name='selector3')
selector3.inputs.index = original_list[:-3]
selector4 = pe.Node(niu.Select(), name='selector3')
selector4.inputs.index = original_list[:-4]
wf_connections = [(selector1, selector2, [('out', 'inlist')]), (selector2, selector3, [('out', 'inlist')]), (selector3, selector4, [('out', 'inlist')])]
with pytest.raises(IOError) as excinfo:
    wf.connect(wf_connections)
assert 'Duplicate node name "selector3" found.' == str(excinfo.value)
```

## Next Steps


---

*Source: test_workflows.py:101 | Complexity: Advanced | Last updated: 2026-05-18*