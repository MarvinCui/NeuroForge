# How To: To Mask

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test to mask

## Prerequisites

**Required Modules:**
- `math`
- `pathlib`
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.affines`
- `nibabel.fileslice`
- `nibabel.optpkg`
- `nibabel.spatialimages`
- `nibabel.tests.nibabel_data`


## Step-by-Step Guide

### Step 1: Assign coords = np.array(...)

```python
coords = np.array([[1, 1, 1]])
```

**Verification:**
```python
assert mask_img.shape == (2, 2, 2)
```

### Step 2: Assign grid = ps.Grid(...)

```python
grid = ps.Grid(coords)
```

**Verification:**
```python
assert np.array_equal(mask_img.get_fdata(), [[[0, 0], [0, 0]], [[0, 0], [0, 1]]])
```

### Step 3: Assign mask_img = grid.to_mask(...)

```python
mask_img = grid.to_mask()
```

**Verification:**
```python
assert np.array_equal(mask_img.affine, np.eye(4))
```

### Step 4: Assign mask_img = grid.to_mask(...)

```python
mask_img = grid.to_mask(shape=(3, 3, 3))
```

**Verification:**
```python
assert mask_img.shape == (3, 3, 3)
```


## Complete Example

```python
# Workflow
coords = np.array([[1, 1, 1]])
grid = ps.Grid(coords)
mask_img = grid.to_mask()
assert mask_img.shape == (2, 2, 2)
assert np.array_equal(mask_img.get_fdata(), [[[0, 0], [0, 0]], [[0, 0], [0, 1]]])
assert np.array_equal(mask_img.affine, np.eye(4))
mask_img = grid.to_mask(shape=(3, 3, 3))
assert mask_img.shape == (3, 3, 3)
assert np.array_equal(mask_img.get_fdata(), [[[0, 0, 0], [0, 0, 0], [0, 0, 0]], [[0, 0, 0], [0, 1, 0], [0, 0, 0]], [[0, 0, 0], [0, 0, 0], [0, 0, 0]]])
assert np.array_equal(mask_img.affine, np.eye(4))
```

## Next Steps


---

*Source: test_pointset.py:161 | Complexity: Intermediate | Last updated: 2026-05-18*