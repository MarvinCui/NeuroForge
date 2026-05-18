# How To: Vector Cosine

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test vector cosine

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.sphere_stats`
- `dipy.testing.decorators`
- `dipy.testing.spherepoints`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign a = value

```python
a = [0, 1]
```

**Verification:**
```python
assert_array_almost_equal(vector_cosine(a, b), 0)
```

### Step 2: Assign b = value

```python
b = [1, 0]
```

**Verification:**
```python
assert_array_almost_equal(vector_cosine([1, 0], [-1, 0]), -1)
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(vector_cosine(a, b), 0)
```

**Verification:**
```python
assert_array_almost_equal(vector_cosine([1, 0], [1, 1]), 1 / np.sqrt(2))
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(vector_cosine([1, 0], [-1, 0]), -1)
```

**Verification:**
```python
assert_array_almost_equal(vector_cosine([2, 0], [-4, 0]), -1)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(vector_cosine([1, 0], [1, 1]), 1 / np.sqrt(2))
```

**Verification:**
```python
assert_array_almost_equal(vector_cosine(pts1, pts2), -1)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(vector_cosine([2, 0], [-4, 0]), -1)
```

**Verification:**
```python
assert_array_almost_equal(vector_cosine(pts1, pts2), [-1, 1])
```

### Step 7: Assign pts1 = value

```python
pts1 = [2, 1, 0]
```

**Verification:**
```python
assert not np.allclose(cc, vcos)
```

### Step 8: Assign pts2 = value

```python
pts2 = [-2, -1, 0]
```

**Verification:**
```python
assert_array_almost_equal(cc, vcos)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(vector_cosine(pts1, pts2), -1)
```

### Step 10: Assign pts2 = value

```python
pts2 = [[-2, -1, 0], [2, 1, 0]]
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(vector_cosine(pts1, pts2), [-1, 1])
```

### Step 12: Assign a = rng.uniform(...)

```python
a = rng.uniform(size=(100,))
```

### Step 13: Assign b = rng.uniform(...)

```python
b = rng.uniform(size=(100,))
```

### Step 14: Assign cc = value

```python
cc = np.corrcoef(a, b)[0, 1]
```

### Step 15: Assign vcos = vector_cosine(...)

```python
vcos = vector_cosine(a, b)
```

**Verification:**
```python
assert not np.allclose(cc, vcos)
```

### Step 16: Assign a_dm = value

```python
a_dm = a - np.mean(a)
```

### Step 17: Assign b_dm = value

```python
b_dm = b - np.mean(b)
```

### Step 18: Assign vcos = vector_cosine(...)

```python
vcos = vector_cosine(a_dm, b_dm)
```

### Step 19: Call assert_array_almost_equal()

```python
assert_array_almost_equal(cc, vcos)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
a = [0, 1]
b = [1, 0]
assert_array_almost_equal(vector_cosine(a, b), 0)
assert_array_almost_equal(vector_cosine([1, 0], [-1, 0]), -1)
assert_array_almost_equal(vector_cosine([1, 0], [1, 1]), 1 / np.sqrt(2))
assert_array_almost_equal(vector_cosine([2, 0], [-4, 0]), -1)
pts1 = [2, 1, 0]
pts2 = [-2, -1, 0]
assert_array_almost_equal(vector_cosine(pts1, pts2), -1)
pts2 = [[-2, -1, 0], [2, 1, 0]]
assert_array_almost_equal(vector_cosine(pts1, pts2), [-1, 1])
a = rng.uniform(size=(100,))
b = rng.uniform(size=(100,))
cc = np.corrcoef(a, b)[0, 1]
vcos = vector_cosine(a, b)
assert not np.allclose(cc, vcos)
a_dm = a - np.mean(a)
b_dm = b - np.mean(b)
vcos = vector_cosine(a_dm, b_dm)
assert_array_almost_equal(cc, vcos)
```

## Next Steps


---

*Source: test_geometry.py:153 | Complexity: Advanced | Last updated: 2026-05-18*