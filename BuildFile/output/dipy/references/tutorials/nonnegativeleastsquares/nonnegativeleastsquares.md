# How To: Nonnegativeleastsquares

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nonnegativeleastsquares

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `scipy.sparse`
- `dipy.core.optimize`
- `dipy.core.optimize`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign n = 100

```python
n = 100
```

### Step 2: Assign X = np.eye(...)

```python
X = np.eye(n)
```

### Step 3: Assign beta = rng.random(...)

```python
beta = rng.random(n)
```

### Step 4: Assign y = np.dot(...)

```python
y = np.dot(X, beta)
```

### Step 5: Assign my_nnls = opt.NonNegativeLeastSquares(...)

```python
my_nnls = opt.NonNegativeLeastSquares()
```

### Step 6: Call my_nnls.fit()

```python
my_nnls.fit(X, y)
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(my_nnls.coef_, beta)
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(my_nnls.predict(X), y)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
n = 100
X = np.eye(n)
beta = rng.random(n)
y = np.dot(X, beta)
my_nnls = opt.NonNegativeLeastSquares()
my_nnls.fit(X, y)
npt.assert_equal(my_nnls.coef_, beta)
npt.assert_equal(my_nnls.predict(X), y)
```

## Next Steps


---

*Source: test_optimize.py:88 | Complexity: Advanced | Last updated: 2026-05-18*