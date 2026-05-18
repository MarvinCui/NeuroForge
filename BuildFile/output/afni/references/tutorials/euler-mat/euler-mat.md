# How To: Euler Mat

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test euler mat

## Prerequisites

**Required Modules:**
- `math`
- `numpy`
- `numpy`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign M = nea.euler2mat(...)

```python
M = nea.euler2mat()
```

### Step 2: yield (assert_array_equal, M, np.eye(3))

```python
yield (assert_array_equal, M, np.eye(3))
```

### Step 3: Assign M1 = nea.euler2mat(...)

```python
M1 = nea.euler2mat(z, y, x)
```

### Step 4: Assign M2 = sympy_euler(...)

```python
M2 = sympy_euler(z, y, x)
```

### Step 5: yield (assert_array_almost_equal, M1, M2)

```python
yield (assert_array_almost_equal, M1, M2)
```

### Step 6: Assign M3 = np.dot(...)

```python
M3 = np.dot(x_only(x), np.dot(y_only(y), z_only(z)))
```

### Step 7: yield (assert_array_almost_equal, M1, M3)

```python
yield (assert_array_almost_equal, M1, M3)
```

### Step 8: Assign unknown = nea.mat2euler(...)

```python
zp, yp, xp = nea.mat2euler(M1)
```

### Step 9: Assign M4 = nea.euler2mat(...)

```python
M4 = nea.euler2mat(zp, yp, xp)
```

### Step 10: yield (assert_array_almost_equal, M1, M4)

```python
yield (assert_array_almost_equal, M1, M4)
```


## Complete Example

```python
# Workflow
M = nea.euler2mat()
yield (assert_array_equal, M, np.eye(3))
for x, y, z in eg_rots:
    M1 = nea.euler2mat(z, y, x)
    M2 = sympy_euler(z, y, x)
    yield (assert_array_almost_equal, M1, M2)
    M3 = np.dot(x_only(x), np.dot(y_only(y), z_only(z)))
    yield (assert_array_almost_equal, M1, M3)
    zp, yp, xp = nea.mat2euler(M1)
    M4 = nea.euler2mat(zp, yp, xp)
    yield (assert_array_almost_equal, M1, M4)
```

## Next Steps


---

*Source: test_euler.py:106 | Complexity: Advanced | Last updated: 2026-05-18*