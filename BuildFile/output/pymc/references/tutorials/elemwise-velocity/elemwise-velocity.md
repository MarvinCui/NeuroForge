# How To: Elemwise Velocity

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test elemwise velocity

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.sparse`
- `pymc`
- `pymc.pytensorf`
- `pymc.step_methods.hmc`


## Step-by-Step Guide

### Step 1: Assign scaling = np.array(...)

```python
scaling = np.array([1, 2, 3])
```

**Verification:**
```python
assert v.dtype == pot.dtype
```

### Step 2: Assign x = floatX(...)

```python
x = floatX(np.ones_like(scaling))
```

### Step 3: Assign pot = quadpotential.quad_potential(...)

```python
pot = quadpotential.quad_potential(scaling, True)
```

### Step 4: Assign v = pot.velocity(...)

```python
v = pot.velocity(x)
```

### Step 5: Call npt.assert_allclose()

```python
npt.assert_allclose(v, scaling)
```

**Verification:**
```python
assert v.dtype == pot.dtype
```


## Complete Example

```python
# Workflow
scaling = np.array([1, 2, 3])
x = floatX(np.ones_like(scaling))
pot = quadpotential.quad_potential(scaling, True)
v = pot.velocity(x)
npt.assert_allclose(v, scaling)
assert v.dtype == pot.dtype
```

## Next Steps


---

*Source: test_quadpotential.py:33 | Complexity: Intermediate | Last updated: 2026-05-18*