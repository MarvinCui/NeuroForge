# How To: Warning All Voxels Masked Thresholding

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Warn when all values are masked due to thresholding.

Also return the center of mass is returned.

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

### Step 1: 'Warn when all values are masked due to thresholding.\n\n    Also return the center of mass is returned.\n    '

```python
'Warn when all values are masked due to thresholding.\n\n    Also return the center of mass is returned.\n    '
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

### Step 6: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask_data, affine_eye)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(cut_coords, [4.5, 4.5, 4.5])
```

### Step 8: Assign cut_coords = find_xyz_cut_coords(...)

```python
cut_coords = find_xyz_cut_coords(img, mask_img=mask_img, activation_threshold=10 ** 3)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Warn when all values are masked due to thresholding.\n\n    Also return the center of mass is returned.\n    '
data = np.zeros((20, 20, 20))
data[4:6, 4:6, 4:6] = 1000
img = Nifti1Image(data, affine_eye)
mask_data = np.ones((20, 20, 20), dtype='uint8')
mask_img = Nifti1Image(mask_data, affine_eye)
with pytest.warns(UserWarning, match='Could not determine cut coords: All voxels were masked by the thresholding.'):
    cut_coords = find_xyz_cut_coords(img, mask_img=mask_img, activation_threshold=10 ** 3)
assert_array_equal(cut_coords, [4.5, 4.5, 4.5])
```

## Next Steps


---

*Source: test_find_cuts.py:108 | Complexity: Advanced | Last updated: 2026-05-18*