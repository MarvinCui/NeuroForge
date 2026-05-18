# How To: Find Probabilistic Atlas Cut Coords

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test find_probabilistic_atlas_cut_coords with simple affine.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `nilearn.masking`
- `nilearn.plotting.find_cuts`

**Setup Required:**
```python
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: 'Test find_probabilistic_atlas_cut_coords with simple affine.'

```python
'Test find_probabilistic_atlas_cut_coords with simple affine.'
```

**Verification:**
```python
assert (n_maps, 3) == coords.shape
```

### Step 2: Assign unknown = value

```python
x_map_a, y_map_a, z_map_a = (30, 40, 50)
```

**Verification:**
```python
assert_allclose((coords[0][0], coords[0][1], coords[0][2]), (x_map_a, y_map_a, z_map_a), rtol=0.06)
```

### Step 3: Assign unknown = value

```python
x_map_b, y_map_b, z_map_b = (40, 50, 60)
```

**Verification:**
```python
assert_allclose((coords[2][0], coords[2][1], coords[2][2]), (x_map_b - 0.5, y_map_b - 0.5, z_map_b - 0.5), rtol=0.06)
```

### Step 4: Assign data = _proba_parcellation_2_roi(...)

```python
data = _proba_parcellation_2_roi(x_map_a, y_map_a, z_map_a, x_map_b, y_map_b, z_map_b)
```

### Step 5: Assign n_maps = value

```python
n_maps = data.shape[-1]
```

### Step 6: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 7: Assign coords = find_probabilistic_atlas_cut_coords(...)

```python
coords = find_probabilistic_atlas_cut_coords(img)
```

**Verification:**
```python
assert (n_maps, 3) == coords.shape
```

### Step 8: Call assert_allclose()

```python
assert_allclose((coords[0][0], coords[0][1], coords[0][2]), (x_map_a, y_map_a, z_map_a), rtol=0.06)
```

### Step 9: Call assert_allclose()

```python
assert_allclose((coords[2][0], coords[2][1], coords[2][2]), (x_map_b - 0.5, y_map_b - 0.5, z_map_b - 0.5), rtol=0.06)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Test find_probabilistic_atlas_cut_coords with simple affine.'
x_map_a, y_map_a, z_map_a = (30, 40, 50)
x_map_b, y_map_b, z_map_b = (40, 50, 60)
data = _proba_parcellation_2_roi(x_map_a, y_map_a, z_map_a, x_map_b, y_map_b, z_map_b)
n_maps = data.shape[-1]
img = Nifti1Image(data, affine_eye)
coords = find_probabilistic_atlas_cut_coords(img)
assert (n_maps, 3) == coords.shape
assert_allclose((coords[0][0], coords[0][1], coords[0][2]), (x_map_a, y_map_a, z_map_a), rtol=0.06)
assert_allclose((coords[2][0], coords[2][1], coords[2][2]), (x_map_b - 0.5, y_map_b - 0.5, z_map_b - 0.5), rtol=0.06)
```

## Next Steps


---

*Source: test_find_cuts.py:524 | Complexity: Advanced | Last updated: 2026-05-18*