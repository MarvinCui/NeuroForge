# How To: Cut Plane

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cut plane

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking.streamline`
- `time`


## Step-by-Step Guide

### Step 1: Assign dt = np.dtype(...)

```python
dt = np.dtype(np.float32)
```

**Verification:**
```python
assert_array_almost_equal(hitx[0], expected_hit0)
```

### Step 2: Assign refx = np.array(...)

```python
refx = np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0], [3, 0, 0]], dtype=dt)
```

**Verification:**
```python
assert_array_almost_equal(hitx[1], expected_hit1)
```

### Step 3: Assign bundlex = value

```python
bundlex = [np.array([[0.5, 1, 0], [1.5, 2, 0], [2.5, 3, 0]], dtype=dt), np.array([[0.5, 2, 0], [1.5, 3, 0], [2.5, 4, 0]], dtype=dt), np.array([[0.5, 1, 1], [1.5, 2, 2], [2.5, 3, 3]], dtype=dt), np.array([[-0.5, 2, -1], [-1.5, 3, -2], [-2.5, 4, -3]], dtype=dt)]
```

**Verification:**
```python
assert_array_almost_equal(hitx[0], expected_hit0)
```

### Step 4: Assign expected_hit0 = value

```python
expected_hit0 = [[1.0, 1.5, 0.0, 0.70710683, 0.0], [1.0, 2.5, 0.0, 0.70710677, 1.0], [1.0, 1.5, 1.5, 0.81649661, 2.0]]
```

**Verification:**
```python
assert_array_almost_equal(hitx[1], expected_hit1)
```

### Step 5: Assign expected_hit1 = value

```python
expected_hit1 = [[2.0, 2.5, 0.0, 0.70710677, 0.0], [2.0, 3.5, 0.0, 0.70710677, 1.0], [2.0, 2.5, 2.5, 0.81649655, 2.0]]
```

**Verification:**
```python
assert_array_almost_equal(hitx[0], expected_hit0)
```

### Step 6: Assign hitx = pf.cut_plane(...)

```python
hitx = pf.cut_plane(bundlex, refx)
```

**Verification:**
```python
assert_array_almost_equal(hitx[1], expected_hit1)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hitx[0], expected_hit0)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hitx[1], expected_hit1)
```

### Step 9: Assign unknown = np.asarray(...)

```python
bundlex[0] = np.asarray(bundlex[0], dtype=np.float64)
```

### Step 10: Assign hitx = pf.cut_plane(...)

```python
hitx = pf.cut_plane(bundlex, refx)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hitx[0], expected_hit0)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hitx[1], expected_hit1)
```

### Step 13: Assign refx = np.asarray(...)

```python
refx = np.asarray(refx, dtype=np.float64)
```

### Step 14: Assign hitx = pf.cut_plane(...)

```python
hitx = pf.cut_plane(bundlex, refx)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hitx[0], expected_hit0)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hitx[1], expected_hit1)
```


## Complete Example

```python
# Workflow
dt = np.dtype(np.float32)
refx = np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0], [3, 0, 0]], dtype=dt)
bundlex = [np.array([[0.5, 1, 0], [1.5, 2, 0], [2.5, 3, 0]], dtype=dt), np.array([[0.5, 2, 0], [1.5, 3, 0], [2.5, 4, 0]], dtype=dt), np.array([[0.5, 1, 1], [1.5, 2, 2], [2.5, 3, 3]], dtype=dt), np.array([[-0.5, 2, -1], [-1.5, 3, -2], [-2.5, 4, -3]], dtype=dt)]
expected_hit0 = [[1.0, 1.5, 0.0, 0.70710683, 0.0], [1.0, 2.5, 0.0, 0.70710677, 1.0], [1.0, 1.5, 1.5, 0.81649661, 2.0]]
expected_hit1 = [[2.0, 2.5, 0.0, 0.70710677, 0.0], [2.0, 3.5, 0.0, 0.70710677, 1.0], [2.0, 2.5, 2.5, 0.81649655, 2.0]]
hitx = pf.cut_plane(bundlex, refx)
assert_array_almost_equal(hitx[0], expected_hit0)
assert_array_almost_equal(hitx[1], expected_hit1)
bundlex[0] = np.asarray(bundlex[0], dtype=np.float64)
hitx = pf.cut_plane(bundlex, refx)
assert_array_almost_equal(hitx[0], expected_hit0)
assert_array_almost_equal(hitx[1], expected_hit1)
refx = np.asarray(refx, dtype=np.float64)
hitx = pf.cut_plane(bundlex, refx)
assert_array_almost_equal(hitx[0], expected_hit0)
assert_array_almost_equal(hitx[1], expected_hit1)
```

## Next Steps


---

*Source: test_distances.py:315 | Complexity: Advanced | Last updated: 2026-05-18*