# How To: Full Adapt Update Window

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test full adapt update window

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.sparse`
- `pymc`
- `pymc.pytensorf`
- `pymc.step_methods.hmc`

**Setup Required:**
```python
# Fixtures: seed
```

## Step-by-Step Guide

### Step 1: Call np.random.seed()

```python
np.random.seed(seed)
```

**Verification:**
```python
assert np.allclose(pot._cov, init_cov)
```

### Step 2: Assign init_cov = np.array(...)

```python
init_cov = np.array([[1.0, 0.02], [0.02, 0.8]])
```

**Verification:**
```python
assert np.allclose(pot._cov, init_cov)
```

### Step 3: Call pot.update()

```python
pot.update(np.random.randn(2), None, True)
```

**Verification:**
```python
assert not np.allclose(pot._cov, init_cov)
```

### Step 4: Assign pot = quadpotential.QuadPotentialFullAdapt(...)

```python
pot = quadpotential.QuadPotentialFullAdapt(2, np.zeros(2), init_cov, 1, update_window=50)
```

### Step 5: Call pot.update()

```python
pot.update(np.random.randn(2), None, True)
```


## Complete Example

```python
# Setup
# Fixtures: seed

# Workflow
np.random.seed(seed)
init_cov = np.array([[1.0, 0.02], [0.02, 0.8]])
with pytest.warns(UserWarning, match='experimental feature'):
    pot = quadpotential.QuadPotentialFullAdapt(2, np.zeros(2), init_cov, 1, update_window=50)
assert np.allclose(pot._cov, init_cov)
for i in range(49):
    pot.update(np.random.randn(2), None, True)
assert np.allclose(pot._cov, init_cov)
pot.update(np.random.randn(2), None, True)
assert not np.allclose(pot._cov, init_cov)
```

## Next Steps


---

*Source: test_quadpotential.py:223 | Complexity: Intermediate | Last updated: 2026-05-18*