# How To: Elemwise Energy

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test elemwise energy

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

### Step 2: Assign x = floatX(...)

```python
x = floatX(np.ones_like(scaling))
```

### Step 3: Assign pot = quadpotential.quad_potential(...)

```python
pot = quadpotential.quad_potential(scaling, True)
```

### Step 4: Assign energy = pot.energy(...)

```python
energy = pot.energy(x)
```

### Step 5: Call npt.assert_allclose()

```python
npt.assert_allclose(energy, 0.5 * scaling.sum())
```


## Complete Example

```python
# Workflow
scaling = np.array([1, 2, 3])
x = floatX(np.ones_like(scaling))
pot = quadpotential.quad_potential(scaling, True)
energy = pot.energy(x)
npt.assert_allclose(energy, 0.5 * scaling.sum())
```

## Next Steps


---

*Source: test_quadpotential.py:42 | Complexity: Intermediate | Last updated: 2026-05-18*