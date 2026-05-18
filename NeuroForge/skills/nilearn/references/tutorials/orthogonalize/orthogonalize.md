# How To: Orthogonalize

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that the orthogonalization is OK.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm.first_level.hemodynamic_models`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test that the orthogonalization is OK.'

```python
'Test that the orthogonalization is OK.'
```

**Verification:**
```python
assert_almost_equal((K ** 2).sum(), 0, 15)
```

### Step 2: Assign X = rng.standard_normal(...)

```python
X = rng.standard_normal(size=(100, 5))
```

### Step 3: Assign X = orthogonalize(...)

```python
X = orthogonalize(X)
```

### Step 4: Assign K = np.dot(...)

```python
K = np.dot(X.T, X)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal((K ** 2).sum(), 0, 15)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test that the orthogonalization is OK.'
X = rng.standard_normal(size=(100, 5))
X = orthogonalize(X)
K = np.dot(X.T, X)
K -= np.diag(np.diag(K))
assert_almost_equal((K ** 2).sum(), 0, 15)
```

## Next Steps


---

*Source: test_hemodynamic_models.py:82 | Complexity: Intermediate | Last updated: 2026-05-18*