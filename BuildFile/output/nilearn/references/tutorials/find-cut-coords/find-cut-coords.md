# How To: Find Cut Coords

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test find_xyz_cut_coords.

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

### Step 1: 'Test find_xyz_cut_coords.'

```python
'Test find_xyz_cut_coords.'
```

**Verification:**
```python
assert_allclose((x, y, z), (x_map, y_map, z_map), rtol=0.06)
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((100, 100, 100))
```

**Verification:**
```python
assert_allclose((x, y, z), (x_map / 2.0, y_map / 3.0, z_map / 4.0), rtol=0.06)
```

### Step 3: Assign unknown = value

```python
x_map, y_map, z_map = (50, 10, 40)
```

### Step 4: Assign unknown = 1

```python
data[x_map - 30:x_map + 30, y_map - 3:y_map + 3, z_map - 10:z_map + 10] = 1
```

### Step 5: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 6: Assign mask_img = compute_epi_mask(...)

```python
mask_img = compute_epi_mask(img)
```

### Step 7: Assign unknown = find_xyz_cut_coords(...)

```python
x, y, z = find_xyz_cut_coords(img, mask_img=mask_img)
```

### Step 8: Call assert_allclose()

```python
assert_allclose((x, y, z), (x_map, y_map, z_map), rtol=0.06)
```

### Step 9: Assign affine = np.diag(...)

```python
affine = np.diag([1.0 / 2, 1 / 3.0, 1 / 4.0, 1.0])
```

### Step 10: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine)
```

### Step 11: Assign mask_img = compute_epi_mask(...)

```python
mask_img = compute_epi_mask(img)
```

### Step 12: Assign unknown = find_xyz_cut_coords(...)

```python
x, y, z = find_xyz_cut_coords(img, mask_img=mask_img)
```

### Step 13: Call assert_allclose()

```python
assert_allclose((x, y, z), (x_map / 2.0, y_map / 3.0, z_map / 4.0), rtol=0.06)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Test find_xyz_cut_coords.'
data = np.zeros((100, 100, 100))
x_map, y_map, z_map = (50, 10, 40)
data[x_map - 30:x_map + 30, y_map - 3:y_map + 3, z_map - 10:z_map + 10] = 1
img = Nifti1Image(data, affine_eye)
mask_img = compute_epi_mask(img)
x, y, z = find_xyz_cut_coords(img, mask_img=mask_img)
assert_allclose((x, y, z), (x_map, y_map, z_map), rtol=0.06)
affine = np.diag([1.0 / 2, 1 / 3.0, 1 / 4.0, 1.0])
img = Nifti1Image(data, affine)
mask_img = compute_epi_mask(img)
x, y, z = find_xyz_cut_coords(img, mask_img=mask_img)
assert_allclose((x, y, z), (x_map / 2.0, y_map / 3.0, z_map / 4.0), rtol=0.06)
```

## Next Steps


---

*Source: test_find_cuts.py:17 | Complexity: Advanced | Last updated: 2026-05-18*