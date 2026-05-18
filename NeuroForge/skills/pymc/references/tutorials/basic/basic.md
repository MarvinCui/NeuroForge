# How To: Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test basic

## Prerequisites

**Required Modules:**
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor.compile.builders`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc.distributions.distribution`
- `pymc.initial_point`


## Step-by-Step Guide

### Step 1: Assign rv = pm.Normal.dist(...)

```python
rv = pm.Normal.dist(mu=2.3)
```

**Verification:**
```python
assert support_point(rv).eval() == np.zeros(())
```

### Step 2: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(support_point(rv).eval(), 2.3)
```

**Verification:**
```python
assert support_point(rv).eval() == np.ones(())
```

### Step 3: Assign rv = pm.Flat.dist(...)

```python
rv = pm.Flat.dist()
```

**Verification:**
```python
assert np.all(support_point(rv).eval() == np.zeros((2, 4)))
```

### Step 4: Assign rv = pm.HalfFlat.dist(...)

```python
rv = pm.HalfFlat.dist()
```

**Verification:**
```python
assert np.all(support_point(rv).eval() == np.ones((2, 4)))
```

### Step 5: Assign rv = pm.Flat.dist(...)

```python
rv = pm.Flat.dist(size=(2, 4))
```

**Verification:**
```python
assert np.all(support_point(rv).eval() == np.zeros((2, 4)))
```

### Step 6: Assign rv = pm.HalfFlat.dist(...)

```python
rv = pm.HalfFlat.dist(size=(2, 4))
```

**Verification:**
```python
assert np.all(support_point(rv).eval() == np.ones((2, 4)))
```


## Complete Example

```python
# Workflow
rv = pm.Normal.dist(mu=2.3)
np.testing.assert_allclose(support_point(rv).eval(), 2.3)
rv = pm.Flat.dist()
assert support_point(rv).eval() == np.zeros(())
rv = pm.HalfFlat.dist()
assert support_point(rv).eval() == np.ones(())
rv = pm.Flat.dist(size=(2, 4))
assert np.all(support_point(rv).eval() == np.zeros((2, 4)))
rv = pm.HalfFlat.dist(size=(2, 4))
assert np.all(support_point(rv).eval() == np.ones((2, 4)))
```

## Next Steps


---

*Source: test_initial_point.py:241 | Complexity: Intermediate | Last updated: 2026-05-18*