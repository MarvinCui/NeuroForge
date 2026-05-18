# How To: Multiple Fast Inv

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test multiple fast inv

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.linalg`
- `scipy.stats`
- `numpy.testing`
- `scipy.stats`
- `nilearn._utils.data_gen`
- `nilearn.glm._utils`
- `nilearn.glm.first_level`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (10, 20, 20)
```

**Verification:**
```python
assert_almost_equal(X_inv_ref, X_inv)
```

### Step 2: Assign X = rng.standard_normal(...)

```python
X = rng.standard_normal(size=shape)
```

### Step 3: Assign X_inv_ref = np.zeros(...)

```python
X_inv_ref = np.zeros(shape)
```

### Step 4: Assign X_inv = multiple_fast_inverse(...)

```python
X_inv = multiple_fast_inverse(X)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(X_inv_ref, X_inv)
```

### Step 6: Assign unknown = np.dot(...)

```python
X[i] = np.dot(X[i], X[i].T)
```

### Step 7: Assign unknown = spl.inv(...)

```python
X_inv_ref[i] = spl.inv(X[i])
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
shape = (10, 20, 20)
X = rng.standard_normal(size=shape)
X_inv_ref = np.zeros(shape)
for i in range(shape[0]):
    X[i] = np.dot(X[i], X[i].T)
    X_inv_ref[i] = spl.inv(X[i])
X_inv = multiple_fast_inverse(X)
assert_almost_equal(X_inv_ref, X_inv)
```

## Next Steps


---

*Source: test_utils.py:205 | Complexity: Intermediate | Last updated: 2026-05-18*