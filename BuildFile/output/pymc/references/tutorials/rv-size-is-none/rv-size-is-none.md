# How To: Rv Size Is None

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rv size is none

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

### Step 1: Assign rv = pm.Normal.dist(...)

```python
rv = pm.Normal.dist(0, 1, size=None)
```

**Verification:**
```python
assert rv_size_is_none(rv.owner.inputs[1])
```

### Step 2: Assign rv = pm.Normal.dist(...)

```python
rv = pm.Normal.dist(0, 1, size=())
```

**Verification:**
```python
assert not rv_size_is_none(rv.owner.inputs[1])
```

### Step 3: Assign rv = pm.Normal.dist(...)

```python
rv = pm.Normal.dist(0, 1, size=1)
```

**Verification:**
```python
assert not rv_size_is_none(rv.owner.inputs[1])
```

### Step 4: Assign size = pm.Bernoulli.dist(...)

```python
size = pm.Bernoulli.dist(0.5)
```

**Verification:**
```python
assert not rv_size_is_none(rv.owner.inputs[1])
```

### Step 5: Assign rv = pm.Normal.dist(...)

```python
rv = pm.Normal.dist(0, 1, size=size)
```

**Verification:**
```python
assert not rv_size_is_none(rv.owner.inputs[1])
```

### Step 6: Assign size = value

```python
size = pm.Normal.dist(0, 1).size
```

### Step 7: Assign rv = pm.Normal.dist(...)

```python
rv = pm.Normal.dist(0, 1, size=size)
```

**Verification:**
```python
assert not rv_size_is_none(rv.owner.inputs[1])
```


## Complete Example

```python
# Workflow
rv = pm.Normal.dist(0, 1, size=None)
assert rv_size_is_none(rv.owner.inputs[1])
rv = pm.Normal.dist(0, 1, size=())
assert not rv_size_is_none(rv.owner.inputs[1])
rv = pm.Normal.dist(0, 1, size=1)
assert not rv_size_is_none(rv.owner.inputs[1])
size = pm.Bernoulli.dist(0.5)
rv = pm.Normal.dist(0, 1, size=size)
assert not rv_size_is_none(rv.owner.inputs[1])
size = pm.Normal.dist(0, 1).size
rv = pm.Normal.dist(0, 1, size=size)
assert not rv_size_is_none(rv.owner.inputs[1])
```

## Next Steps


---

*Source: test_shape_utils.py:369 | Complexity: Intermediate | Last updated: 2026-05-18*