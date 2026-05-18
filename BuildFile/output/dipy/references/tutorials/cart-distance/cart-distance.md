# How To: Cart Distance

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cart distance

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

### Step 1: Assign a = value

```python
a = [0, 1]
```

**Verification:**
```python
assert_array_almost_equal(cart_distance(a, b), np.sqrt(2))
```

### Step 2: Assign b = value

```python
b = [1, 0]
```

**Verification:**
```python
assert_array_almost_equal(cart_distance([1, 0], [-1, 0]), 2)
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(cart_distance(a, b), np.sqrt(2))
```

**Verification:**
```python
assert_array_almost_equal(cart_distance(pts1, pts2), np.sqrt(8))
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(cart_distance([1, 0], [-1, 0]), 2)
```

**Verification:**
```python
assert_array_almost_equal(cart_distance(pts1, pts2), [np.sqrt(8), 4])
```

### Step 5: Assign pts1 = value

```python
pts1 = [2, 1, 0]
```

### Step 6: Assign pts2 = value

```python
pts2 = [0, 1, -2]
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(cart_distance(pts1, pts2), np.sqrt(8))
```

### Step 8: Assign pts2 = value

```python
pts2 = [[0, 1, -2], [-2, 1, 0]]
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(cart_distance(pts1, pts2), [np.sqrt(8), 4])
```


## Complete Example

```python
# Workflow
a = [0, 1]
b = [1, 0]
assert_array_almost_equal(cart_distance(a, b), np.sqrt(2))
assert_array_almost_equal(cart_distance([1, 0], [-1, 0]), 2)
pts1 = [2, 1, 0]
pts2 = [0, 1, -2]
assert_array_almost_equal(cart_distance(pts1, pts2), np.sqrt(8))
pts2 = [[0, 1, -2], [-2, 1, 0]]
assert_array_almost_equal(cart_distance(pts1, pts2), [np.sqrt(8), 4])
```

## Next Steps


---

*Source: test_geometry.py:109 | Complexity: Advanced | Last updated: 2026-05-18*