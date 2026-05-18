# How To: Affines

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test affines

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
# Fixtures: shape, homogeneous
```

## Step-by-Step Guide

### Step 1: Assign orig_coords, coords = self.rng.random(...)

```python
orig_coords = coords = self.rng.random(shape)
```

**Verification:**
```python
assert np.allclose(points.get_coords(), orig_coords)
```

### Step 2: Assign points = ps.Pointset(...)

```python
points = ps.Pointset(coords, homogeneous=homogeneous)
```

**Verification:**
```python
assert np.array_equal(scaled.coordinates, points.coordinates)
```

### Step 3: Assign scaler = np.diag(...)

```python
scaler = np.diag([2] * shape[1] + [1])
```

**Verification:**
```python
assert np.array_equal(scaled.affine, scaler)
```

### Step 4: Assign scaled = value

```python
scaled = scaler @ points
```

**Verification:**
```python
assert np.allclose(scaled.get_coords(), 2 * orig_coords)
```

### Step 5: Assign flipper = np.eye(...)

```python
flipper = np.eye(shape[1] + 1)
```

**Verification:**
```python
assert np.array_equal(flipped.coordinates, points.coordinates)
```

### Step 6: Assign unknown = value

```python
flipper[:-1] = flipper[-2::-1]
```

**Verification:**
```python
assert np.array_equal(flipped.affine, flipper)
```

### Step 7: Assign flipped = value

```python
flipped = flipper @ points
```

**Verification:**
```python
assert np.allclose(flipped.get_coords(), orig_coords[:, ::-1])
```

### Step 8: Assign coords = np.column_stack(...)

```python
coords = np.column_stack([coords, np.ones(shape[0])])
```

**Verification:**
```python
assert np.array_equal(doubledup.coordinates, points.coordinates)
```


## Complete Example

```python
# Setup
# Fixtures: shape, homogeneous

# Workflow
orig_coords = coords = self.rng.random(shape)
if homogeneous:
    coords = np.column_stack([coords, np.ones(shape[0])])
points = ps.Pointset(coords, homogeneous=homogeneous)
assert np.allclose(points.get_coords(), orig_coords)
scaler = np.diag([2] * shape[1] + [1])
scaled = scaler @ points
assert np.array_equal(scaled.coordinates, points.coordinates)
assert np.array_equal(scaled.affine, scaler)
assert np.allclose(scaled.get_coords(), 2 * orig_coords)
flipper = np.eye(shape[1] + 1)
flipper[:-1] = flipper[-2::-1]
flipped = flipper @ points
assert np.array_equal(flipped.coordinates, points.coordinates)
assert np.array_equal(flipped.affine, flipper)
assert np.allclose(flipped.get_coords(), orig_coords[:, ::-1])
for doubledup in [scaler @ flipper @ points, scaler @ (flipper @ points)]:
    assert np.array_equal(doubledup.coordinates, points.coordinates)
    assert np.allclose(doubledup.affine, scaler @ flipper)
    assert np.allclose(doubledup.get_coords(), 2 * orig_coords[:, ::-1])
```

## Next Steps


---

*Source: test_pointset.py:50 | Complexity: Advanced | Last updated: 2026-05-18*