# How To: Pos Recipr

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test pos recipr

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign X = np.array(...)

```python
X = np.array([2, 1, -1, 0], dtype=np.int8)
```

**Verification:**
```python
assert_array_almost_equal(Y, eX)
```

### Step 2: Assign eX = np.array(...)

```python
eX = np.array([0.5, 1, 0, 0])
```

**Verification:**
```python
assert Y.dtype.type == np.float64
```

### Step 3: Assign Y = positive_reciprocal(...)

```python
Y = positive_reciprocal(X)
```

**Verification:**
```python
assert_array_almost_equal(Y2, eX.reshape((2, 2)))
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(Y, eX)
```

**Verification:**
```python
assert_array_almost_equal(positive_reciprocal(XL), [0, 1, 0])
```

### Step 5: Assign X2 = X.reshape(...)

```python
X2 = X.reshape((2, 2))
```

**Verification:**
```python
assert positive_reciprocal(-1) == 0
```

### Step 6: Assign Y2 = positive_reciprocal(...)

```python
Y2 = positive_reciprocal(X2)
```

**Verification:**
```python
assert positive_reciprocal(0) == 0
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(Y2, eX.reshape((2, 2)))
```

**Verification:**
```python
assert positive_reciprocal(2) == 0.5
```

### Step 8: Assign XL = value

```python
XL = [0, 1, -1]
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(positive_reciprocal(XL), [0, 1, 0])
```

**Verification:**
```python
assert positive_reciprocal(-1) == 0
```


## Complete Example

```python
# Workflow
X = np.array([2, 1, -1, 0], dtype=np.int8)
eX = np.array([0.5, 1, 0, 0])
Y = positive_reciprocal(X)
assert_array_almost_equal(Y, eX)
assert Y.dtype.type == np.float64
X2 = X.reshape((2, 2))
Y2 = positive_reciprocal(X2)
assert_array_almost_equal(Y2, eX.reshape((2, 2)))
XL = [0, 1, -1]
assert_array_almost_equal(positive_reciprocal(XL), [0, 1, 0])
assert positive_reciprocal(-1) == 0
assert positive_reciprocal(0) == 0
assert positive_reciprocal(2) == 0.5
```

## Next Steps


---

*Source: test_utils.py:231 | Complexity: Advanced | Last updated: 2026-05-18*