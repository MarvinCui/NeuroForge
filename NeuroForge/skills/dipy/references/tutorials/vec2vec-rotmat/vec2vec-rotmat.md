# How To: Vec2Vec Rotmat

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test vec2vec rotmat

## Prerequisites

**Required Modules:**
- `itertools`
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.sphere_stats`
- `dipy.testing.decorators`
- `dipy.testing.spherepoints`


## Step-by-Step Guide

### Step 1: Assign a = np.array(...)

```python
a = np.array([1, 0, 0])
```

**Verification:**
```python
assert_array_almost_equal(np.dot(R, a), b)
```

### Step 2: Assign c = np.array(...)

```python
c = np.array([0.33950729, 0.92041729, 0.1938216])
```

**Verification:**
```python
assert_array_almost_equal(R1, R2, decimal=1)
```

### Step 3: Assign d = np.array(...)

```python
d = np.array([0.40604787, 0.97518325, 0.2057731])
```

**Verification:**
```python
assert_array_almost_equal(np.diag(R1), np.diag(R2), decimal=3)
```

### Step 4: Assign R1 = vec2vec_rotmat(...)

```python
R1 = vec2vec_rotmat(c, d)
```

**Verification:**
```python
assert_array_almost_equal(R3, R4, decimal=1)
```

### Step 5: Assign c_norm = value

```python
c_norm = c / np.linalg.norm(c)
```

**Verification:**
```python
assert_array_almost_equal(np.diag(R3), np.diag(R4), decimal=3)
```

### Step 6: Assign d_norm = value

```python
d_norm = d / np.linalg.norm(d)
```

### Step 7: Assign R2 = vec2vec_rotmat(...)

```python
R2 = vec2vec_rotmat(c_norm, d_norm)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(R1, R2, decimal=1)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.diag(R1), np.diag(R2), decimal=3)
```

### Step 10: Assign e = np.array(...)

```python
e = np.array([1.0001, 0, 0])
```

### Step 11: Assign f = np.array(...)

```python
f = np.array([1.001, 0.01, 0])
```

### Step 12: Assign R3 = vec2vec_rotmat(...)

```python
R3 = vec2vec_rotmat(e, f)
```

### Step 13: Assign g = np.array(...)

```python
g = np.array([1.001, 0.0, 0])
```

### Step 14: Assign R4 = vec2vec_rotmat(...)

```python
R4 = vec2vec_rotmat(e, g)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(R3, R4, decimal=1)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.diag(R3), np.diag(R4), decimal=3)
```

### Step 17: Assign R = vec2vec_rotmat(...)

```python
R = vec2vec_rotmat(a, b)
```

### Step 18: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.dot(R, a), b)
```


## Complete Example

```python
# Workflow
a = np.array([1, 0, 0])
for b in np.array([[0, 0, 1], [-1, 0, 0], [1, 0, 0]]):
    R = vec2vec_rotmat(a, b)
    assert_array_almost_equal(np.dot(R, a), b)
c = np.array([0.33950729, 0.92041729, 0.1938216])
d = np.array([0.40604787, 0.97518325, 0.2057731])
R1 = vec2vec_rotmat(c, d)
c_norm = c / np.linalg.norm(c)
d_norm = d / np.linalg.norm(d)
R2 = vec2vec_rotmat(c_norm, d_norm)
assert_array_almost_equal(R1, R2, decimal=1)
assert_array_almost_equal(np.diag(R1), np.diag(R2), decimal=3)
e = np.array([1.0001, 0, 0])
f = np.array([1.001, 0.01, 0])
R3 = vec2vec_rotmat(e, f)
g = np.array([1.001, 0.0, 0])
R4 = vec2vec_rotmat(e, g)
assert_array_almost_equal(R3, R4, decimal=1)
assert_array_almost_equal(np.diag(R3), np.diag(R4), decimal=3)
```

## Next Steps


---

*Source: test_geometry.py:216 | Complexity: Advanced | Last updated: 2026-05-18*