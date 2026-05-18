# How To: Mapnode Iterfield Type

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test mapnode iterfield type

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
# Fixtures: x_inp, f_exp
```

## Step-by-Step Guide

### Step 1: Assign double = Function(...)

```python
double = Function(['x'], ['f_x'], double_func)
```

**Verification:**
```python
assert res.outputs.f_x == f_exp
```

### Step 2: Assign double_node = MapNode(...)

```python
double_node = MapNode(double, name='double', iterfield=['x'])
```

### Step 3: Assign double_node.inputs.x = x_inp

```python
double_node.inputs.x = x_inp
```

### Step 4: Assign res = double_node.run(...)

```python
res = double_node.run()
```

**Verification:**
```python
assert res.outputs.f_x == f_exp
```


## Complete Example

```python
# Setup
# Fixtures: x_inp, f_exp

# Workflow
from nipype import MapNode, Function

def double_func(x):
    return 2 * x
double = Function(['x'], ['f_x'], double_func)
double_node = MapNode(double, name='double', iterfield=['x'])
double_node.inputs.x = x_inp
res = double_node.run()
assert res.outputs.f_x == f_exp
```

## Next Steps


---

*Source: test_nodes.py:127 | Complexity: Intermediate | Last updated: 2026-05-18*