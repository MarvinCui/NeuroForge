# How To: Apply Affine

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test apply affine

## Prerequisites

**Required Modules:**
- `numpy`
- `affines`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(20110903)
```

**Verification:**
```python
assert_array_equal(apply_affine(aff, pts), pts * [[2, 3, 4]])
```

### Step 2: Assign aff = np.diag(...)

```python
aff = np.diag([2, 3, 4, 1])
```

**Verification:**
```python
assert_array_equal(apply_affine(aff, pts), pts * [[2, 3, 4]] + [[10, 11, 12]])
```

### Step 3: Assign pts = rng.uniform(...)

```python
pts = rng.uniform(size=(4, 3))
```

**Verification:**
```python
assert_array_equal(apply_affine(aff, pts), exp_res)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(apply_affine(aff, pts), pts * [[2, 3, 4]])
```

**Verification:**
```python
assert_almost_equal(validated_apply_affine(aff, pts), apply_affine(aff, pts))
```

### Step 5: Assign unknown = value

```python
aff[:3, 3] = [10, 11, 12]
```

**Verification:**
```python
assert_array_equal(apply_affine(aff.tolist(), pts.tolist()), exp_res)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(apply_affine(aff, pts), pts * [[2, 3, 4]] + [[10, 11, 12]])
```

**Verification:**
```python
assert_array_equal(apply_affine(aff, pts), exp_res)
```

### Step 7: Assign unknown = rng.normal(...)

```python
aff[:3, :] = rng.normal(size=(3, 4))
```

**Verification:**
```python
assert_array_equal(apply_affine(aff, pts), exp_res)
```

### Step 8: Assign exp_res = np.concatenate(...)

```python
exp_res = np.concatenate((pts.T, np.ones((1, 4))), axis=0)
```

**Verification:**
```python
assert_array_almost_equal(res, exp_res)
```

### Step 9: Assign exp_res = value

```python
exp_res = np.dot(aff, exp_res)[:3, :].T
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(apply_affine(aff, pts), exp_res)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(validated_apply_affine(aff, pts), apply_affine(aff, pts))
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(apply_affine(aff.tolist(), pts.tolist()), exp_res)
```

### Step 13: Assign aff = np.array(...)

```python
aff = np.array([[0, 2, 0, 10], [3, 0, 0, 11], [0, 0, 4, 12], [0, 0, 0, 1]])
```

### Step 14: Assign pts = np.array(...)

```python
pts = np.array([[1, 2, 3], [2, 3, 4], [4, 5, 6], [6, 7, 8]])
```

### Step 15: Assign exp_res = value

```python
exp_res = (np.dot(aff[:3, :3], pts.T) + aff[:3, 3:4]).T
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(apply_affine(aff, pts), exp_res)
```

### Step 17: Assign pts = pts.reshape(...)

```python
pts = pts.reshape((2, 2, 3))
```

### Step 18: Assign exp_res = exp_res.reshape(...)

```python
exp_res = exp_res.reshape((2, 2, 3))
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(apply_affine(aff, pts), exp_res)
```

### Step 20: Assign aff = np.eye(...)

```python
aff = np.eye(N)
```

### Step 21: Assign nd = value

```python
nd = N - 1
```

### Step 22: Assign unknown = rng.normal(...)

```python
aff[:nd, :nd] = rng.normal(size=(nd, nd))
```

### Step 23: Assign pts = rng.normal(...)

```python
pts = rng.normal(size=(2, 3, nd))
```

### Step 24: Assign res = apply_affine(...)

```python
res = apply_affine(aff, pts)
```

### Step 25: Assign new_pts = np.ones(...)

```python
new_pts = np.ones((N, 6))
```

### Step 26: Assign unknown = np.rollaxis.reshape(...)

```python
new_pts[:-1, :] = np.rollaxis(pts, -1).reshape((nd, 6))
```

### Step 27: Assign exp_pts = np.dot(...)

```python
exp_pts = np.dot(aff, new_pts)
```

### Step 28: Assign exp_pts = np.rollaxis(...)

```python
exp_pts = np.rollaxis(exp_pts[:-1, :], 0, 2)
```

### Step 29: Assign exp_res = exp_pts.reshape(...)

```python
exp_res = exp_pts.reshape((2, 3, nd))
```

### Step 30: Call assert_array_almost_equal()

```python
assert_array_almost_equal(res, exp_res)
```


## Complete Example

```python
# Workflow
rng = np.random.RandomState(20110903)
aff = np.diag([2, 3, 4, 1])
pts = rng.uniform(size=(4, 3))
assert_array_equal(apply_affine(aff, pts), pts * [[2, 3, 4]])
aff[:3, 3] = [10, 11, 12]
assert_array_equal(apply_affine(aff, pts), pts * [[2, 3, 4]] + [[10, 11, 12]])
aff[:3, :] = rng.normal(size=(3, 4))
exp_res = np.concatenate((pts.T, np.ones((1, 4))), axis=0)
exp_res = np.dot(aff, exp_res)[:3, :].T
assert_array_equal(apply_affine(aff, pts), exp_res)
assert_almost_equal(validated_apply_affine(aff, pts), apply_affine(aff, pts))
assert_array_equal(apply_affine(aff.tolist(), pts.tolist()), exp_res)
aff = np.array([[0, 2, 0, 10], [3, 0, 0, 11], [0, 0, 4, 12], [0, 0, 0, 1]])
pts = np.array([[1, 2, 3], [2, 3, 4], [4, 5, 6], [6, 7, 8]])
exp_res = (np.dot(aff[:3, :3], pts.T) + aff[:3, 3:4]).T
assert_array_equal(apply_affine(aff, pts), exp_res)
pts = pts.reshape((2, 2, 3))
exp_res = exp_res.reshape((2, 2, 3))
assert_array_equal(apply_affine(aff, pts), exp_res)
for N in range(2, 6):
    aff = np.eye(N)
    nd = N - 1
    aff[:nd, :nd] = rng.normal(size=(nd, nd))
    pts = rng.normal(size=(2, 3, nd))
    res = apply_affine(aff, pts)
    new_pts = np.ones((N, 6))
    new_pts[:-1, :] = np.rollaxis(pts, -1).reshape((nd, 6))
    exp_pts = np.dot(aff, new_pts)
    exp_pts = np.rollaxis(exp_pts[:-1, :], 0, 2)
    exp_res = exp_pts.reshape((2, 3, nd))
    assert_array_almost_equal(res, exp_res)
```

## Next Steps


---

*Source: test_affines.py:27 | Complexity: Advanced | Last updated: 2026-05-18*