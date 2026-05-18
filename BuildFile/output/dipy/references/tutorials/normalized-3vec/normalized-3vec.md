# How To: Normalized 3Vec

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test normalized 3vec

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`


## Step-by-Step Guide

### Step 1: Assign vec = value

```python
vec = [1, 2, 3]
```

**Verification:**
```python
assert_array_almost_equal(l2n, pf.norm_3vec(vec))
```

### Step 2: Assign l2n = np.sqrt(...)

```python
l2n = np.sqrt(np.dot(vec, vec))
```

**Verification:**
```python
assert_array_almost_equal(np.array(vec) / l2n, nvec)
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(l2n, pf.norm_3vec(vec))
```

**Verification:**
```python
assert_equal(vec.shape, (1, 3))
```

### Step 4: Assign nvec = pf.normalized_3vec(...)

```python
nvec = pf.normalized_3vec(vec)
```

**Verification:**
```python
assert_equal(pf.normalized_3vec(vec).shape, (3,))
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.array(vec) / l2n, nvec)
```

### Step 6: Assign vec = np.array(...)

```python
vec = np.array([[1, 2, 3]])
```

### Step 7: Call assert_equal()

```python
assert_equal(vec.shape, (1, 3))
```

### Step 8: Call assert_equal()

```python
assert_equal(pf.normalized_3vec(vec).shape, (3,))
```


## Complete Example

```python
# Workflow
vec = [1, 2, 3]
l2n = np.sqrt(np.dot(vec, vec))
assert_array_almost_equal(l2n, pf.norm_3vec(vec))
nvec = pf.normalized_3vec(vec)
assert_array_almost_equal(np.array(vec) / l2n, nvec)
vec = np.array([[1, 2, 3]])
assert_equal(vec.shape, (1, 3))
assert_equal(pf.normalized_3vec(vec).shape, (3,))
```

## Next Steps


---

*Source: test_metrics.py:41 | Complexity: Advanced | Last updated: 2026-05-18*