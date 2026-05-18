# How To: Voxel Sizes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test voxel sizes

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `pytest`
- `numpy.testing`
- `affines`
- `eulerangles`
- `orientations`
- `math`


## Step-by-Step Guide

### Step 1: Assign affine = np.diag(...)

```python
affine = np.diag([2, 3, 4, 1])
```

**Verification:**
```python
assert_almost_equal(voxel_sizes(affine), [2, 3, 4])
```

### Step 2: Call assert_almost_equal()

```python
assert_almost_equal(voxel_sizes(affine), [2, 3, 4])
```

**Verification:**
```python
assert_almost_equal(voxel_sizes(aff), vox_sizes)
```

### Step 3: Assign rotations = value

```python
rotations = []
```

**Verification:**
```python
assert_almost_equal(voxel_sizes(aff), vox_sizes)
```

### Step 4: Call rotations.append()

```python
rotations.append(euler2mat(z_rot, y_rot, x_rot))
```

**Verification:**
```python
assert_almost_equal(voxel_sizes(new_row), vox_sizes)
```

### Step 5: Assign vox_sizes = value

```python
vox_sizes = np.arange(n) + 4.1
```

**Verification:**
```python
assert_almost_equal(voxel_sizes(new_col), [0] + list(vox_sizes))
```

### Step 6: Assign aff = np.diag(...)

```python
aff = np.diag(list(vox_sizes) + [1])
```

**Verification:**
```python
assert_almost_equal(voxel_sizes(full_aff), vox_sizes)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(voxel_sizes(aff), vox_sizes)
```

### Step 8: Assign unknown = value

```python
aff[:-1, -1] = np.arange(n) + 10
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(voxel_sizes(aff), vox_sizes)
```

### Step 10: Assign new_row = np.vstack(...)

```python
new_row = np.vstack((np.zeros(n + 1), aff))
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(voxel_sizes(new_row), vox_sizes)
```

### Step 12: Assign new_col = value

```python
new_col = np.c_[np.zeros(n + 1), aff]
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(voxel_sizes(new_col), [0] + list(vox_sizes))
```

### Step 14: Assign rot_affine = np.eye(...)

```python
rot_affine = np.eye(n + 1)
```

### Step 15: Assign unknown = rotation

```python
rot_affine[:3, :3] = rotation
```

### Step 16: Assign full_aff = rot_affine.dot(...)

```python
full_aff = rot_affine.dot(aff)
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(voxel_sizes(full_aff), vox_sizes)
```


## Complete Example

```python
# Workflow
affine = np.diag([2, 3, 4, 1])
assert_almost_equal(voxel_sizes(affine), [2, 3, 4])
rotations = []
for x_rot, y_rot, z_rot in product((0, 0.4), (0, 0.6), (0, 0.8)):
    rotations.append(euler2mat(z_rot, y_rot, x_rot))
for n in range(2, 10):
    vox_sizes = np.arange(n) + 4.1
    aff = np.diag(list(vox_sizes) + [1])
    assert_almost_equal(voxel_sizes(aff), vox_sizes)
    aff[:-1, -1] = np.arange(n) + 10
    assert_almost_equal(voxel_sizes(aff), vox_sizes)
    new_row = np.vstack((np.zeros(n + 1), aff))
    assert_almost_equal(voxel_sizes(new_row), vox_sizes)
    new_col = np.c_[np.zeros(n + 1), aff]
    assert_almost_equal(voxel_sizes(new_col), [0] + list(vox_sizes))
    if n < 3:
        continue
    for rotation in rotations:
        rot_affine = np.eye(n + 1)
        rot_affine[:3, :3] = rotation
        full_aff = rot_affine.dot(aff)
        assert_almost_equal(voxel_sizes(full_aff), vox_sizes)
```

## Next Steps


---

*Source: test_affines.py:181 | Complexity: Advanced | Last updated: 2026-05-18*