# How To: Euler Mat 2

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test euler mat 2

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `math`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`

**Setup Required:**
```python
# Fixtures: x, y, z
```

## Step-by-Step Guide

### Step 1: Assign M1 = nea.euler2mat(...)

```python
M1 = nea.euler2mat(z, y, x)
```

**Verification:**
```python
assert_array_almost_equal(M1, M2)
```

### Step 2: Assign M2 = sympy_euler(...)

```python
M2 = sympy_euler(z, y, x)
```

**Verification:**
```python
assert_array_almost_equal(M1, M3)
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(M1, M2)
```

**Verification:**
```python
assert_array_almost_equal(M1, M4)
```

### Step 4: Assign M3 = np.dot(...)

```python
M3 = np.dot(x_only(x), np.dot(y_only(y), z_only(z)))
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(M1, M3)
```

### Step 6: Assign unknown = nea.mat2euler(...)

```python
zp, yp, xp = nea.mat2euler(M1)
```

### Step 7: Assign M4 = nea.euler2mat(...)

```python
M4 = nea.euler2mat(zp, yp, xp)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(M1, M4)
```


## Complete Example

```python
# Setup
# Fixtures: x, y, z

# Workflow
M1 = nea.euler2mat(z, y, x)
M2 = sympy_euler(z, y, x)
assert_array_almost_equal(M1, M2)
M3 = np.dot(x_only(x), np.dot(y_only(y), z_only(z)))
assert_array_almost_equal(M1, M3)
zp, yp, xp = nea.mat2euler(M1)
M4 = nea.euler2mat(zp, yp, xp)
assert_array_almost_equal(M1, M4)
```

## Next Steps


---

*Source: test_euler.py:123 | Complexity: Advanced | Last updated: 2026-05-18*