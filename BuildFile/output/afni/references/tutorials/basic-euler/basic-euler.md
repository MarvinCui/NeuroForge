# How To: Basic Euler

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test basic euler

## Prerequisites

**Required Modules:**
- `math`
- `numpy`
- `numpy`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign zr = 0.05

```python
zr = 0.05
```

### Step 2: Assign yr = value

```python
yr = -0.4
```

### Step 3: Assign xr = 0.2

```python
xr = 0.2
```

### Step 4: Assign M = nea.euler2mat(...)

```python
M = nea.euler2mat(zr, yr, xr)
```

### Step 5: Assign M1 = nea.euler2mat(...)

```python
M1 = nea.euler2mat(zr)
```

### Step 6: Assign M2 = nea.euler2mat(...)

```python
M2 = nea.euler2mat(0, yr)
```

### Step 7: Assign M3 = nea.euler2mat(...)

```python
M3 = nea.euler2mat(0, 0, xr)
```

### Step 8: yield (assert_true, is_valid_rotation(M))

```python
yield (assert_true, is_valid_rotation(M))
```

### Step 9: yield (assert_true, is_valid_rotation(M1))

```python
yield (assert_true, is_valid_rotation(M1))
```

### Step 10: yield (assert_true, is_valid_rotation(M2))

```python
yield (assert_true, is_valid_rotation(M2))
```

### Step 11: yield (assert_true, is_valid_rotation(M3))

```python
yield (assert_true, is_valid_rotation(M3))
```

### Step 12: yield (assert_true, np.allclose(M, np.dot(M3, np.dot(M2, M1))))

```python
yield (assert_true, np.allclose(M, np.dot(M3, np.dot(M2, M1))))
```

### Step 13: yield (assert_true, np.all(nea.euler2mat(zr) == nea.euler2mat(z=zr)))

```python
yield (assert_true, np.all(nea.euler2mat(zr) == nea.euler2mat(z=zr)))
```

### Step 14: yield (assert_true, np.all(nea.euler2mat(0, yr) == nea.euler2mat(y=yr)))

```python
yield (assert_true, np.all(nea.euler2mat(0, yr) == nea.euler2mat(y=yr)))
```

### Step 15: yield (assert_true, np.all(nea.euler2mat(0, 0, xr) == nea.euler2mat(x=xr)))

```python
yield (assert_true, np.all(nea.euler2mat(0, 0, xr) == nea.euler2mat(x=xr)))
```

### Step 16: yield (assert_true, np.allclose(nea.euler2mat(x=-xr), np.linalg.inv(nea.euler2mat(x=xr))))

```python
yield (assert_true, np.allclose(nea.euler2mat(x=-xr), np.linalg.inv(nea.euler2mat(x=xr))))
```


## Complete Example

```python
# Workflow
zr = 0.05
yr = -0.4
xr = 0.2
M = nea.euler2mat(zr, yr, xr)
M1 = nea.euler2mat(zr)
M2 = nea.euler2mat(0, yr)
M3 = nea.euler2mat(0, 0, xr)
yield (assert_true, is_valid_rotation(M))
yield (assert_true, is_valid_rotation(M1))
yield (assert_true, is_valid_rotation(M2))
yield (assert_true, is_valid_rotation(M3))
yield (assert_true, np.allclose(M, np.dot(M3, np.dot(M2, M1))))
yield (assert_true, np.all(nea.euler2mat(zr) == nea.euler2mat(z=zr)))
yield (assert_true, np.all(nea.euler2mat(0, yr) == nea.euler2mat(y=yr)))
yield (assert_true, np.all(nea.euler2mat(0, 0, xr) == nea.euler2mat(x=xr)))
yield (assert_true, np.allclose(nea.euler2mat(x=-xr), np.linalg.inv(nea.euler2mat(x=xr))))
```

## Next Steps


---

*Source: test_euler.py:78 | Complexity: Advanced | Last updated: 2026-05-18*