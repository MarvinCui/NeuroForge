# How To: Basic Euler

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test basic euler

## Prerequisites

**Required Modules:**
- `math`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign zr = 0.05

```python
zr = 0.05
```

**Verification:**
```python
assert is_valid_rotation(M)
```

### Step 2: Assign yr = value

```python
yr = -0.4
```

**Verification:**
```python
assert is_valid_rotation(M1)
```

### Step 3: Assign xr = 0.2

```python
xr = 0.2
```

**Verification:**
```python
assert is_valid_rotation(M2)
```

### Step 4: Assign M = nea.euler2mat(...)

```python
M = nea.euler2mat(zr, yr, xr)
```

**Verification:**
```python
assert is_valid_rotation(M3)
```

### Step 5: Assign M1 = nea.euler2mat(...)

```python
M1 = nea.euler2mat(zr)
```

**Verification:**
```python
assert np.allclose(M, np.dot(M3, np.dot(M2, M1)))
```

### Step 6: Assign M2 = nea.euler2mat(...)

```python
M2 = nea.euler2mat(0, yr)
```

**Verification:**
```python
assert np.all(nea.euler2mat(zr) == nea.euler2mat(z=zr))
```

### Step 7: Assign M3 = nea.euler2mat(...)

```python
M3 = nea.euler2mat(0, 0, xr)
```

**Verification:**
```python
assert np.all(nea.euler2mat(0, yr) == nea.euler2mat(y=yr))
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
assert is_valid_rotation(M)
assert is_valid_rotation(M1)
assert is_valid_rotation(M2)
assert is_valid_rotation(M3)
assert np.allclose(M, np.dot(M3, np.dot(M2, M1)))
assert np.all(nea.euler2mat(zr) == nea.euler2mat(z=zr))
assert np.all(nea.euler2mat(0, yr) == nea.euler2mat(y=yr))
assert np.all(nea.euler2mat(0, 0, xr) == nea.euler2mat(x=xr))
assert np.allclose(nea.euler2mat(x=-xr), np.linalg.inv(nea.euler2mat(x=xr)))
```

## Next Steps


---

*Source: test_euler.py:90 | Complexity: Intermediate | Last updated: 2026-05-18*