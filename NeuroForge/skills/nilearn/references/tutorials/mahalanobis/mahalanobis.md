# How To: Mahalanobis

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mahalanobis

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

### Step 1: Assign n = 50

```python
n = 50
```

**Verification:**
```python
assert_almost_equal(mah, multiple_mahalanobis(x, A), decimal=1)
```

### Step 2: Assign x = value

```python
x = rng.uniform(size=n) / n
```

### Step 3: Assign A = value

```python
A = rng.uniform(size=(n, n)) / n
```

### Step 4: Assign A = value

```python
A = np.dot(A.transpose(), A) + np.eye(n)
```

### Step 5: Assign mah = np.dot(...)

```python
mah = np.dot(x, np.dot(spl.inv(A), x))
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(mah, multiple_mahalanobis(x, A), decimal=1)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
n = 50
x = rng.uniform(size=n) / n
A = rng.uniform(size=(n, n)) / n
A = np.dot(A.transpose(), A) + np.eye(n)
mah = np.dot(x, np.dot(spl.inv(A), x))
assert_almost_equal(mah, multiple_mahalanobis(x, A), decimal=1)
```

## Next Steps


---

*Source: test_utils.py:164 | Complexity: Intermediate | Last updated: 2026-05-18*