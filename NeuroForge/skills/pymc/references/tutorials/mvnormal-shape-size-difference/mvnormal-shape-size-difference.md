# How To: Mvnormal Shape Size Difference

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mvnormal shape size difference

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

### Step 1: Assign rv = pm.MvNormal.dist(...)

```python
rv = pm.MvNormal.dist(mu=np.ones((4, 3)), cov=np.eye(3), shape=(4, 3))
```

**Verification:**
```python
assert rv.ndim == 2
```

### Step 2: Assign rv = pm.MvNormal.dist(...)

```python
rv = pm.MvNormal.dist(mu=[1, 2, 3], cov=np.eye(3), shape=(5, 4, 3))
```

**Verification:**
```python
assert tuple(rv.shape.eval()) == (4, 3)
```

### Step 3: Assign rv = pm.MvNormal.dist(...)

```python
rv = pm.MvNormal.dist(mu=np.ones((4, 3)), cov=np.eye(3), shape=(5, 4, 3))
```

**Verification:**
```python
assert rv.ndim == 3
```

### Step 4: Assign rv = pm.MvNormal.dist(...)

```python
rv = pm.MvNormal.dist(mu=[1, 2, 3], cov=np.eye(3), size=(5, 4))
```

**Verification:**
```python
assert tuple(rv.shape.eval()) == (5, 4, 3)
```

### Step 5: Assign rv = pm.MvNormal.dist(...)

```python
rv = pm.MvNormal.dist(mu=np.ones((5, 4, 3)), cov=np.eye(3), size=(5, 4))
```

**Verification:**
```python
assert rv.ndim == 3
```


## Complete Example

```python
# Workflow
rv = pm.MvNormal.dist(mu=np.ones((4, 3)), cov=np.eye(3), shape=(4, 3))
assert rv.ndim == 2
assert tuple(rv.shape.eval()) == (4, 3)
rv = pm.MvNormal.dist(mu=[1, 2, 3], cov=np.eye(3), shape=(5, 4, 3))
assert rv.ndim == 3
assert tuple(rv.shape.eval()) == (5, 4, 3)
rv = pm.MvNormal.dist(mu=np.ones((4, 3)), cov=np.eye(3), shape=(5, 4, 3))
assert rv.ndim == 3
assert tuple(rv.shape.eval()) == (5, 4, 3)
rv = pm.MvNormal.dist(mu=[1, 2, 3], cov=np.eye(3), size=(5, 4))
assert tuple(rv.shape.eval()) == (5, 4, 3)
rv = pm.MvNormal.dist(mu=np.ones((5, 4, 3)), cov=np.eye(3), size=(5, 4))
assert tuple(rv.shape.eval()) == (5, 4, 3)
```

## Next Steps


---

*Source: test_shape_utils.py:269 | Complexity: Intermediate | Last updated: 2026-05-18*