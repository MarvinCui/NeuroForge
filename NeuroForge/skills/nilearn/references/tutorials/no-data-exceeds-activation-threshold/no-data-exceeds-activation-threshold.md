# How To: No Data Exceeds Activation Threshold

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test when no data exceeds the activation threshold.

Cut coords should be the center of mass rather than
the center of the image (10, 10, 10).

regression test
https://github.com/nilearn/nilearn/issues/473

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

### Step 1: 'Test when no data exceeds the activation threshold.\n\n    Cut coords should be the center of mass rather than\n    the center of the image (10, 10, 10).\n\n    regression test\n    https://github.com/nilearn/nilearn/issues/473\n    '

```python
'Test when no data exceeds the activation threshold.\n\n    Cut coords should be the center of mass rather than\n    the center of the image (10, 10, 10).\n\n    regression test\n    https://github.com/nilearn/nilearn/issues/473\n    '
```

**Verification:**
```python
assert_array_equal([x, y, z], [17.5, 21.0, 17.5])
```

### Step 2: Assign data = np.ones(...)

```python
data = np.ones((36, 43, 36))
```

**Verification:**
```python
assert_array_equal(cut_coords, [9.0, 9.0, 9.0])
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal([x, y, z], [17.5, 21.0, 17.5])
```

### Step 5: Assign data = np.zeros(...)

```python
data = np.zeros((20, 20, 20))
```

### Step 6: Assign unknown = 1000

```python
data[4:6, 4:6, 4:6] = 1000
```

### Step 7: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, 2 * affine_eye)
```

### Step 8: Assign mask_data = np.ones(...)

```python
mask_data = np.ones((20, 20, 20), dtype='uint8')
```

### Step 9: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask_data, 2 * affine_eye)
```

### Step 10: Assign cut_coords = find_xyz_cut_coords(...)

```python
cut_coords = find_xyz_cut_coords(img, mask_img=mask_img)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(cut_coords, [9.0, 9.0, 9.0])
```

### Step 12: Assign unknown = find_xyz_cut_coords(...)

```python
x, y, z = find_xyz_cut_coords(img, activation_threshold=1.1)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Test when no data exceeds the activation threshold.\n\n    Cut coords should be the center of mass rather than\n    the center of the image (10, 10, 10).\n\n    regression test\n    https://github.com/nilearn/nilearn/issues/473\n    '
data = np.ones((36, 43, 36))
img = Nifti1Image(data, affine_eye)
with pytest.warns(UserWarning, match='All voxels were masked.'):
    x, y, z = find_xyz_cut_coords(img, activation_threshold=1.1)
assert_array_equal([x, y, z], [17.5, 21.0, 17.5])
data = np.zeros((20, 20, 20))
data[4:6, 4:6, 4:6] = 1000
img = Nifti1Image(data, 2 * affine_eye)
mask_data = np.ones((20, 20, 20), dtype='uint8')
mask_img = Nifti1Image(mask_data, 2 * affine_eye)
cut_coords = find_xyz_cut_coords(img, mask_img=mask_img)
assert_array_equal(cut_coords, [9.0, 9.0, 9.0])
```

## Next Steps


---

*Source: test_find_cuts.py:56 | Complexity: Advanced | Last updated: 2026-05-18*