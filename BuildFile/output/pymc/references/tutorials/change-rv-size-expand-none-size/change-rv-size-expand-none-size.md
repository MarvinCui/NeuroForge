# How To: Change Rv Size Expand None Size

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test change rv size expand none size

## Prerequisites

**Required Modules:**
- `re`
- `warnings`
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor.compile.mode`
- `pytensor.graph`
- `pytensor.tensor`
- `pytensor.tensor.random`
- `pytensor.tensor.shape`
- `pymc`
- `pymc.distributions.shape_utils`
- `pymc.exceptions`
- `pymc.model`
- `pymc.pytensorf`


## Step-by-Step Guide

### Step 1: Assign x = pt.random.normal(...)

```python
x = pt.random.normal()
```

**Verification:**
```python
assert rv_size_is_none(size)
```

### Step 2: Assign size = x.owner.op.size_param(...)

```python
size = x.owner.op.size_param(x.owner)
```

**Verification:**
```python
assert not rv_size_is_none(new_size)
```

### Step 3: Assign new_x = change_dist_size(...)

```python
new_x = change_dist_size(x, new_size=(2,), expand=True)
```

**Verification:**
```python
assert new_size.data == [2]
```

### Step 4: Assign new_size = new_x.owner.op.size_param(...)

```python
new_size = new_x.owner.op.size_param(new_x.owner)
```

**Verification:**
```python
assert new_x.type.shape == (2,)
```


## Complete Example

```python
# Workflow
x = pt.random.normal()
size = x.owner.op.size_param(x.owner)
assert rv_size_is_none(size)
new_x = change_dist_size(x, new_size=(2,), expand=True)
new_size = new_x.owner.op.size_param(new_x.owner)
assert not rv_size_is_none(new_size)
assert new_size.data == [2]
assert new_x.type.shape == (2,)
```

## Next Steps


---

*Source: test_shape_utils.py:439 | Complexity: Intermediate | Last updated: 2026-05-18*