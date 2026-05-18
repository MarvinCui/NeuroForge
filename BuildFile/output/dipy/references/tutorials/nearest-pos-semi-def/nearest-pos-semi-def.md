# How To: Nearest Pos Semi Def

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nearest pos semi def

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

### Step 1: Assign B = np.diag(...)

```python
B = np.diag(np.array([1, 2, 3]))
```

**Verification:**
```python
assert_array_almost_equal(B, nearest_pos_semi_def(B))
```

### Step 2: Call assert_array_almost_equal()

```python
assert_array_almost_equal(B, nearest_pos_semi_def(B))
```

**Verification:**
```python
assert_array_almost_equal(B, nearest_pos_semi_def(B))
```

### Step 3: Assign B = np.diag(...)

```python
B = np.diag(np.array([0, 2, 3]))
```

**Verification:**
```python
assert_array_almost_equal(B, nearest_pos_semi_def(B))
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(B, nearest_pos_semi_def(B))
```

**Verification:**
```python
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
```

### Step 5: Assign B = np.diag(...)

```python
B = np.diag(np.array([0, 0, 3]))
```

**Verification:**
```python
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(B, nearest_pos_semi_def(B))
```

**Verification:**
```python
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
```

### Step 7: Assign B = np.diag(...)

```python
B = np.diag(np.array([-1, 2, 3]))
```

**Verification:**
```python
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
```

### Step 8: Assign Bpsd = np.array(...)

```python
Bpsd = np.array([[0.0, 0.0, 0.0], [0.0, 1.75, 0.0], [0.0, 0.0, 2.75]])
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
```

### Step 10: Assign B = np.diag(...)

```python
B = np.diag(np.array([-1, -2, 3]))
```

### Step 11: Assign Bpsd = np.array(...)

```python
Bpsd = np.array([[0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 2.0]])
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
```

### Step 13: Assign B = np.diag(...)

```python
B = np.diag(np.array([-1e-11, 0, 1000]))
```

### Step 14: Assign Bpsd = np.array(...)

```python
Bpsd = np.array([[0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 1000.0]])
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
```

### Step 16: Assign B = np.diag(...)

```python
B = np.diag(np.array([-1, -2, -3]))
```

### Step 17: Assign Bpsd = np.array(...)

```python
Bpsd = np.array([[0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0]])
```

### Step 18: Call assert_array_almost_equal()

```python
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
```


## Complete Example

```python
# Workflow
B = np.diag(np.array([1, 2, 3]))
assert_array_almost_equal(B, nearest_pos_semi_def(B))
B = np.diag(np.array([0, 2, 3]))
assert_array_almost_equal(B, nearest_pos_semi_def(B))
B = np.diag(np.array([0, 0, 3]))
assert_array_almost_equal(B, nearest_pos_semi_def(B))
B = np.diag(np.array([-1, 2, 3]))
Bpsd = np.array([[0.0, 0.0, 0.0], [0.0, 1.75, 0.0], [0.0, 0.0, 2.75]])
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
B = np.diag(np.array([-1, -2, 3]))
Bpsd = np.array([[0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 2.0]])
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
B = np.diag(np.array([-1e-11, 0, 1000]))
Bpsd = np.array([[0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 1000.0]])
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
B = np.diag(np.array([-1, -2, -3]))
Bpsd = np.array([[0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0]])
assert_array_almost_equal(Bpsd, nearest_pos_semi_def(B))
```

## Next Steps


---

*Source: test_geometry.py:88 | Complexity: Advanced | Last updated: 2026-05-18*