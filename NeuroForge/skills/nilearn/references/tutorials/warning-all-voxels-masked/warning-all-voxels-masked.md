# How To: Warning All Voxels Masked

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Warning when all values are masked.

And that the center of mass is returned.

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

### Step 1: 'Warning when all values are masked.\n\n    And that the center of mass is returned.\n    '

```python
'Warning when all values are masked.\n\n    And that the center of mass is returned.\n    '
```

**Verification:**
```python
assert_array_equal(cut_coords, [4.5, 4.5, 4.5])
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((20, 20, 20))
```

### Step 3: Assign unknown = 1000

```python
data[4:6, 4:6, 4:6] = 1000
```

### Step 4: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 5: Assign mask_data = np.ones(...)

```python
mask_data = np.ones((20, 20, 20), dtype='uint8')
```

### Step 6: Assign unknown = 0

```python
mask_data[np.argwhere(data == 1000)] = 0
```

### Step 7: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask_data, affine_eye)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(cut_coords, [4.5, 4.5, 4.5])
```

### Step 9: Assign cut_coords = find_xyz_cut_coords(...)

```python
cut_coords = find_xyz_cut_coords(img, mask_img=mask_img)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Warning when all values are masked.\n\n    And that the center of mass is returned.\n    '
data = np.zeros((20, 20, 20))
data[4:6, 4:6, 4:6] = 1000
img = Nifti1Image(data, affine_eye)
mask_data = np.ones((20, 20, 20), dtype='uint8')
mask_data[np.argwhere(data == 1000)] = 0
mask_img = Nifti1Image(mask_data, affine_eye)
with pytest.warns(UserWarning, match='Could not determine cut coords: All values were masked.'):
    cut_coords = find_xyz_cut_coords(img, mask_img=mask_img)
assert_array_equal(cut_coords, [4.5, 4.5, 4.5])
```

## Next Steps


---

*Source: test_find_cuts.py:85 | Complexity: Advanced | Last updated: 2026-05-18*