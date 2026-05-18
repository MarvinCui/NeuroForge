# How To: Random Diag

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test random diag

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

### Step 1: Assign d = value

```python
d = np.arange(10) + 1
```

### Step 2: Call np.random.seed()

```python
np.random.seed(42)
```

### Step 3: Assign pots = value

```python
pots = [quadpotential.quad_potential(d, True), quadpotential.quad_potential(1.0 / d, False), quadpotential.quad_potential(np.diag(d), True), quadpotential.quad_potential(np.diag(1.0 / d), False)]
```

### Step 4: Assign d_ = scipy.sparse.csc_matrix(...)

```python
d_ = scipy.sparse.csc_matrix(np.diag(d))
```

### Step 5: Assign pot = quadpotential.quad_potential(...)

```python
pot = quadpotential.quad_potential(d_, True)
```

### Step 6: Call pots.append()

```python
pots.append(pot)
```

### Step 7: Assign vals = np.array(...)

```python
vals = np.array([pot.random() for _ in range(1000)])
```

### Step 8: Call npt.assert_allclose()

```python
npt.assert_allclose(vals.std(0), np.sqrt(1.0 / d), atol=0.1)
```


## Complete Example

```python
# Workflow
d = np.arange(10) + 1
np.random.seed(42)
pots = [quadpotential.quad_potential(d, True), quadpotential.quad_potential(1.0 / d, False), quadpotential.quad_potential(np.diag(d), True), quadpotential.quad_potential(np.diag(1.0 / d), False)]
if quadpotential.chol_available:
    d_ = scipy.sparse.csc_matrix(np.diag(d))
    pot = quadpotential.quad_potential(d_, True)
    pots.append(pot)
for pot in pots:
    vals = np.array([pot.random() for _ in range(1000)])
    npt.assert_allclose(vals.std(0), np.sqrt(1.0 / d), atol=0.1)
```

## Next Steps


---

*Source: test_quadpotential.py:99 | Complexity: Advanced | Last updated: 2026-05-18*