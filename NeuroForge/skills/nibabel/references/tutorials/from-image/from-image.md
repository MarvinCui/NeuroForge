# How To: From Image

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test from image

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: shape
```

## Step-by-Step Guide

### Step 1: Assign affine = np.diag(...)

```python
affine = np.diag([2, 3, 4, 1])
```

**Verification:**
```python
assert grid.n_coords == prod(shape[:3])
```

### Step 2: Assign img = SpatialImage(...)

```python
img = SpatialImage(strided_scalar(shape), affine)
```

**Verification:**
```python
assert grid.dim == 3
```

### Step 3: Assign grid = ps.Grid.from_image(...)

```python
grid = ps.Grid.from_image(img)
```

**Verification:**
```python
assert np.allclose(grid.affine, affine)
```

### Step 4: Assign grid_coords = grid.get_coords(...)

```python
grid_coords = grid.get_coords()
```

**Verification:**
```python
assert np.allclose(grid_coords[0], [0, 0, 0])
```


## Complete Example

```python
# Setup
# Fixtures: shape

# Workflow
affine = np.diag([2, 3, 4, 1])
img = SpatialImage(strided_scalar(shape), affine)
grid = ps.Grid.from_image(img)
grid_coords = grid.get_coords()
assert grid.n_coords == prod(shape[:3])
assert grid.dim == 3
assert np.allclose(grid.affine, affine)
assert np.allclose(grid_coords[0], [0, 0, 0])
assert np.allclose(grid_coords[-1], [8, 12, 16])
```

## Next Steps


---

*Source: test_pointset.py:133 | Complexity: Intermediate | Last updated: 2026-05-18*