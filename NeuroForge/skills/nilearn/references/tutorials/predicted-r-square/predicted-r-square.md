# How To: Predicted R Square

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test predicted r square

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm`

**Setup Required:**
```python
# Fixtures: X, Y
```

## Step-by-Step Guide

### Step 1: Assign Xshort = value

```python
Xshort = X.copy()[:10, :]
```

**Verification:**
```python
assert_almost_equal(results.residuals.sum(), 0)
```

### Step 2: Assign Yshort = value

```python
Yshort = Y.copy()[:10]
```

**Verification:**
```python
assert_array_almost_equal(results.predicted, Yshort)
```

### Step 3: Assign model = OLSModel(...)

```python
model = OLSModel(design=Xshort)
```

**Verification:**
```python
assert_almost_equal(results.r_square, 1.0)
```

### Step 4: Assign results = model.fit(...)

```python
results = model.fit(Yshort)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(results.residuals.sum(), 0)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(results.predicted, Yshort)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(results.r_square, 1.0)
```


## Complete Example

```python
# Setup
# Fixtures: X, Y

# Workflow
Xshort = X.copy()[:10, :]
Yshort = Y.copy()[:10]
model = OLSModel(design=Xshort)
results = model.fit(Yshort)
assert_almost_equal(results.residuals.sum(), 0)
assert_array_almost_equal(results.predicted, Yshort)
assert_almost_equal(results.r_square, 1.0)
```

## Next Steps


---

*Source: test_regression.py:51 | Complexity: Intermediate | Last updated: 2026-05-18*