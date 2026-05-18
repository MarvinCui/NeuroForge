# How To: Quats

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test quats

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
assert nq.nearly_equivalent(quatM, quat)
```

### Step 2: Assign quatM = nq.mat2quat(...)

```python
quatM = nq.mat2quat(M1)
```

**Verification:**
```python
assert nq.nearly_equivalent(quat, quatS)
```

### Step 3: Assign quat = nea.euler2quat(...)

```python
quat = nea.euler2quat(z, y, x)
```

**Verification:**
```python
assert_array_almost_equal(M1, M2)
```

### Step 4: Assign quatS = sympy_euler2quat(...)

```python
quatS = sympy_euler2quat(z, y, x)
```

**Verification:**
```python
assert nq.nearly_equivalent(quat, quatS)
```

### Step 5: Assign unknown = nea.quat2euler(...)

```python
zp, yp, xp = nea.quat2euler(quat)
```

### Step 6: Assign M2 = nea.euler2mat(...)

```python
M2 = nea.euler2mat(zp, yp, xp)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(M1, M2)
```


## Complete Example

```python
# Setup
# Fixtures: x, y, z

# Workflow
M1 = nea.euler2mat(z, y, x)
quatM = nq.mat2quat(M1)
quat = nea.euler2quat(z, y, x)
assert nq.nearly_equivalent(quatM, quat)
quatS = sympy_euler2quat(z, y, x)
assert nq.nearly_equivalent(quat, quatS)
zp, yp, xp = nea.quat2euler(quat)
M2 = nea.euler2mat(zp, yp, xp)
assert_array_almost_equal(M1, M2)
```

## Next Steps


---

*Source: test_euler.py:176 | Complexity: Intermediate | Last updated: 2026-05-18*