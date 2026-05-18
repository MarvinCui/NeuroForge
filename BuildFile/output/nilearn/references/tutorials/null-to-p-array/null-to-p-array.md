# How To: Null To P Array

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test null_to_p with 1d array input.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `math`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.ndimage`
- `nilearn.conftest`
- `nilearn.mass_univariate`
- `nilearn.mass_univariate.tests._testing`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test null_to_p with 1d array input.'

```python
'Test null_to_p with 1d array input.'
```

**Verification:**
```python
assert p.shape == (N,)
```

### Step 2: Assign N = 10000

```python
N = 10000
```

**Verification:**
```python
assert (p < 1).all()
```

### Step 3: Assign nulldist = rng.normal(...)

```python
nulldist = rng.normal(size=N)
```

**Verification:**
```python
assert (p > 0).all()
```

### Step 4: Assign t = np.sort(...)

```python
t = np.sort(rng.normal(size=N))
```

**Verification:**
```python
assert np.abs(p.mean() - 0.5) < 0.02
```

### Step 5: Assign p = np.sort(...)

```python
p = np.sort(_utils.null_to_p(t, nulldist))
```

**Verification:**
```python
assert np.abs(p.var() - 1 / 12) < 0.02
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test null_to_p with 1d array input.'
N = 10000
nulldist = rng.normal(size=N)
t = np.sort(rng.normal(size=N))
p = np.sort(_utils.null_to_p(t, nulldist))
assert p.shape == (N,)
assert (p < 1).all()
assert (p > 0).all()
assert np.abs(p.mean() - 0.5) < 0.02
assert np.abs(p.var() - 1 / 12) < 0.02
```

## Next Steps


---

*Source: test_utils.py:137 | Complexity: Intermediate | Last updated: 2026-05-18*