# How To: Mapnode Nested

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mapnode nested

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `interfaces`
- `interfaces`
- `utils`
- `test_base`
- `test_utils`
- `nipype`
- `nipype`
- `nipype`
- `nipype.interfaces.utility`
- `nipype.pipeline.plugins.base`
- `stat`
- `os`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert n1.get_output('out') == [[2, [3]], 4, [5, 6]]
```

### Step 2: Assign n1 = MapNode(...)

```python
n1 = MapNode(Function(input_names=['in1'], output_names=['out'], function=func1), iterfield=['in1'], nested=True, name='n1')
```

**Verification:**
```python
assert 'can only concatenate list' in str(excinfo.value)
```

### Step 3: Assign n1.inputs.in1 = value

```python
n1.inputs.in1 = [[1, [2]], 3, [4, 5]]
```

### Step 4: Call n1.run()

```python
n1.run()
```

**Verification:**
```python
assert n1.get_output('out') == [[2, [3]], 4, [5, 6]]
```

### Step 5: Assign n2 = MapNode(...)

```python
n2 = MapNode(Function(input_names=['in1'], output_names=['out'], function=func1), iterfield=['in1'], nested=False, name='n1')
```

### Step 6: Assign n2.inputs.in1 = value

```python
n2.inputs.in1 = [[1, [2]], 3, [4, 5]]
```

**Verification:**
```python
assert 'can only concatenate list' in str(excinfo.value)
```

### Step 7: Call n2.run()

```python
n2.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
from nipype import MapNode, Function

def func1(in1):
    return in1 + 1
n1 = MapNode(Function(input_names=['in1'], output_names=['out'], function=func1), iterfield=['in1'], nested=True, name='n1')
n1.inputs.in1 = [[1, [2]], 3, [4, 5]]
n1.run()
assert n1.get_output('out') == [[2, [3]], 4, [5, 6]]
n2 = MapNode(Function(input_names=['in1'], output_names=['out'], function=func1), iterfield=['in1'], nested=False, name='n1')
n2.inputs.in1 = [[1, [2]], 3, [4, 5]]
with pytest.raises(Exception) as excinfo:
    n2.run()
assert 'can only concatenate list' in str(excinfo.value)
```

## Next Steps


---

*Source: test_nodes.py:142 | Complexity: Intermediate | Last updated: 2026-05-18*