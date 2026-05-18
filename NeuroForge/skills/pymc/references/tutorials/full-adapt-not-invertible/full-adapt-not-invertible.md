# How To: Full Adapt Not Invertible

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test full adapt not invertible

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

### Step 1: Assign window = 10

```python
window = 10
```

### Step 2: Assign pot = quadpotential.QuadPotentialFullAdapt(...)

```python
pot = quadpotential.QuadPotentialFullAdapt(2, np.zeros(2), np.eye(2), 0, adaptation_window=window)
```

### Step 3: Call pot.raise_ok()

```python
pot.raise_ok(None)
```

### Step 4: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', 'invalid value encountered in true_divide', RuntimeWarning)
```

### Step 5: Call pot.update()

```python
pot.update(np.ones(2), None, True)
```


## Complete Example

```python
# Workflow
window = 10
with pytest.warns(UserWarning, match='experimental feature'):
    pot = quadpotential.QuadPotentialFullAdapt(2, np.zeros(2), np.eye(2), 0, adaptation_window=window)
for i in range(window + 1):
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', 'invalid value encountered in true_divide', RuntimeWarning)
        pot.update(np.ones(2), None, True)
with pytest.raises(ValueError):
    pot.raise_ok(None)
```

## Next Steps


---

*Source: test_quadpotential.py:258 | Complexity: Intermediate | Last updated: 2026-05-18*