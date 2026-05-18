# How To: Set Boundaries 1D

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test set boundaries 1d

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `arviz`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.spatial`
- `pymc`

**Setup Required:**
```python
# Fixtures: x_min, x_max
```

## Step-by-Step Guide

### Step 1: Assign X1 = value

```python
X1 = np.linspace(x_min, x_max, 100)[:, None]
```

**Verification:**
```python
assert np.allclose(L, expected_L), f'Expected L to be close to {expected_L}, but got {L}'
```

### Step 2: Assign X1s = value

```python
X1s = X1 - np.mean(X1, axis=0)
```

### Step 3: Assign c = 2

```python
c = 2
```

### Step 4: Assign L = pm.gp.hsgp_approx.set_boundary(...)

```python
L = pm.gp.hsgp_approx.set_boundary(X1s, c=c)
```

### Step 5: Assign expected_L = value

```python
expected_L = np.abs(X1.max() - X1.min()) / 2 * c
```

**Verification:**
```python
assert np.allclose(L, expected_L), f'Expected L to be close to {expected_L}, but got {L}'
```


## Complete Example

```python
# Setup
# Fixtures: x_min, x_max

# Workflow
X1 = np.linspace(x_min, x_max, 100)[:, None]
X1s = X1 - np.mean(X1, axis=0)
c = 2
L = pm.gp.hsgp_approx.set_boundary(X1s, c=c)
expected_L = np.abs(X1.max() - X1.min()) / 2 * c
assert np.allclose(L, expected_L), f'Expected L to be close to {expected_L}, but got {L}'
```

## Next Steps


---

*Source: test_hsgp_approx.py:110 | Complexity: Intermediate | Last updated: 2026-05-18*