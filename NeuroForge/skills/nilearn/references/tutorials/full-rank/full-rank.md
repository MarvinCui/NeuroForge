# How To: Full Rank

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test full rank

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

### Step 1: Assign unknown = value

```python
n, p = (10, 5)
```

**Verification:**
```python
assert_array_almost_equal(X, X_)
```

### Step 2: Assign X = rng.standard_normal(...)

```python
X = rng.standard_normal(size=(n, p))
```

**Verification:**
```python
assert cond > 10000000000.0
```

### Step 3: Assign unknown = full_rank(...)

```python
X_, _ = full_rank(X)
```

**Verification:**
```python
assert_array_almost_equal(X, X_)
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(X, X_)
```

### Step 5: Assign unknown = unknown.sum(...)

```python
X[:, -1] = X[:, :-1].sum(1)
```

### Step 6: Assign unknown = full_rank(...)

```python
X_, cond = full_rank(X)
```

**Verification:**
```python
assert cond > 10000000000.0
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(X, X_)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
n, p = (10, 5)
X = rng.standard_normal(size=(n, p))
X_, _ = full_rank(X)
assert_array_almost_equal(X, X_)
X[:, -1] = X[:, :-1].sum(1)
X_, cond = full_rank(X)
assert cond > 10000000000.0
assert_array_almost_equal(X, X_)
```

## Next Steps


---

*Source: test_utils.py:29 | Complexity: Intermediate | Last updated: 2026-05-18*