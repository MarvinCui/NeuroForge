# How To: Homogeneous Coordinates

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test homogeneous coordinates

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

### Step 1: Assign ccoords = self.rng.random(...)

```python
ccoords = self.rng.random((5, 3))
```

**Verification:**
```python
assert np.array_equal(points.get_coords(), ccoords)
```

### Step 2: Assign hcoords = np.column_stack(...)

```python
hcoords = np.column_stack([ccoords, np.ones(5)])
```

**Verification:**
```python
assert np.array_equal(points.get_coords(as_homogeneous=True), hcoords)
```

### Step 3: Assign cartesian = ps.Pointset(...)

```python
cartesian = ps.Pointset(ccoords)
```

**Verification:**
```python
assert np.array_equal(points.get_coords(), exp_c)
```

### Step 4: Assign homogeneous = ps.Pointset(...)

```python
homogeneous = ps.Pointset(hcoords, homogeneous=True)
```

**Verification:**
```python
assert np.array_equal(points.get_coords(as_homogeneous=True), exp_h)
```

### Step 5: Assign affine = np.diag(...)

```python
affine = np.diag([2, 3, 4, 1])
```

### Step 6: Assign cart2 = value

```python
cart2 = affine @ cartesian
```

### Step 7: Assign homo2 = value

```python
homo2 = affine @ homogeneous
```

### Step 8: Assign exp_c = apply_affine(...)

```python
exp_c = apply_affine(affine, ccoords)
```

### Step 9: Assign exp_h = value

```python
exp_h = (affine @ hcoords.T).T
```

**Verification:**
```python
assert np.array_equal(points.get_coords(), ccoords)
```


## Complete Example

```python
# Workflow
ccoords = self.rng.random((5, 3))
hcoords = np.column_stack([ccoords, np.ones(5)])
cartesian = ps.Pointset(ccoords)
homogeneous = ps.Pointset(hcoords, homogeneous=True)
for points in (cartesian, homogeneous):
    assert np.array_equal(points.get_coords(), ccoords)
    assert np.array_equal(points.get_coords(as_homogeneous=True), hcoords)
affine = np.diag([2, 3, 4, 1])
cart2 = affine @ cartesian
homo2 = affine @ homogeneous
exp_c = apply_affine(affine, ccoords)
exp_h = (affine @ hcoords.T).T
for points in (cart2, homo2):
    assert np.array_equal(points.get_coords(), exp_c)
    assert np.array_equal(points.get_coords(as_homogeneous=True), exp_h)
```

## Next Steps


---

*Source: test_pointset.py:80 | Complexity: Advanced | Last updated: 2026-05-18*