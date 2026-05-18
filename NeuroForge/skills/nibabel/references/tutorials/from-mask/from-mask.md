# How To: From Mask

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test from mask

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

### Step 1: Assign affine = np.diag(...)

```python
affine = np.diag([2, 3, 4, 1])
```

**Verification:**
```python
assert grid.n_coords == 1
```

### Step 2: Assign mask = np.zeros(...)

```python
mask = np.zeros((3, 3, 3))
```

**Verification:**
```python
assert grid.dim == 3
```

### Step 3: Assign unknown = 1

```python
mask[1, 1, 1] = 1
```

**Verification:**
```python
assert np.array_equal(grid_coords, [[2, 3, 4]])
```

### Step 4: Assign img = SpatialImage(...)

```python
img = SpatialImage(mask, affine)
```

### Step 5: Assign grid = ps.Grid.from_mask(...)

```python
grid = ps.Grid.from_mask(img)
```

### Step 6: Assign grid_coords = grid.get_coords(...)

```python
grid_coords = grid.get_coords()
```

**Verification:**
```python
assert grid.n_coords == 1
```


## Complete Example

```python
# Workflow
affine = np.diag([2, 3, 4, 1])
mask = np.zeros((3, 3, 3))
mask[1, 1, 1] = 1
img = SpatialImage(mask, affine)
grid = ps.Grid.from_mask(img)
grid_coords = grid.get_coords()
assert grid.n_coords == 1
assert grid.dim == 3
assert np.array_equal(grid_coords, [[2, 3, 4]])
```

## Next Steps


---

*Source: test_pointset.py:148 | Complexity: Intermediate | Last updated: 2026-05-18*