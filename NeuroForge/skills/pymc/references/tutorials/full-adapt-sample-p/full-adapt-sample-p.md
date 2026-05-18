# How To: Full Adapt Sample P

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test full adapt sample p

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

### Step 1: Assign m = np.array(...)

```python
m = np.array([[3.0, -2.0], [-2.0, 4.0]])
```

**Verification:**
```python
assert np.all(np.abs(m - sample_cov) < 5 * np.sqrt(var / n_samples))
```

### Step 2: Assign m_inv = np.linalg.inv(...)

```python
m_inv = np.linalg.inv(m)
```

### Step 3: Assign var = np.array(...)

```python
var = np.array([[2 * m[0, 0] ** 2, m[1, 0] * m[1, 0] + m[1, 1] * m[0, 0]], [m[0, 1] * m[0, 1] + m[1, 1] * m[0, 0], 2 * m[1, 1] ** 2]])
```

### Step 4: Assign n_samples = 1000

```python
n_samples = 1000
```

### Step 5: Assign samples = value

```python
samples = [pot.random() for n in range(n_samples)]
```

### Step 6: Assign sample_cov = np.cov(...)

```python
sample_cov = np.cov(samples, rowvar=0)
```

**Verification:**
```python
assert np.all(np.abs(m - sample_cov) < 5 * np.sqrt(var / n_samples))
```

### Step 7: Assign pot = quadpotential.QuadPotentialFullAdapt(...)

```python
pot = quadpotential.QuadPotentialFullAdapt(2, np.zeros(2), m_inv, 1)
```


## Complete Example

```python
# Workflow
m = np.array([[3.0, -2.0], [-2.0, 4.0]])
m_inv = np.linalg.inv(m)
var = np.array([[2 * m[0, 0] ** 2, m[1, 0] * m[1, 0] + m[1, 1] * m[0, 0]], [m[0, 1] * m[0, 1] + m[1, 1] * m[0, 0], 2 * m[1, 1] ** 2]])
n_samples = 1000
with pytest.warns(UserWarning, match='experimental feature'):
    pot = quadpotential.QuadPotentialFullAdapt(2, np.zeros(2), m_inv, 1)
samples = [pot.random() for n in range(n_samples)]
sample_cov = np.cov(samples, rowvar=0)
assert np.all(np.abs(m - sample_cov) < 5 * np.sqrt(var / n_samples))
```

## Next Steps


---

*Source: test_quadpotential.py:198 | Complexity: Intermediate | Last updated: 2026-05-18*