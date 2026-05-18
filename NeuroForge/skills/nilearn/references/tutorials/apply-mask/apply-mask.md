# How To: Apply Mask

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test smoothing of timeseries extraction.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.preprocessing`
- `nilearn._utils`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.masking`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: tmp_path, create_files, affine
```

## Step-by-Step Guide

### Step 1: 'Test smoothing of timeseries extraction.'

```python
'Test smoothing of timeseries extraction.'
```

**Verification:**
```python
assert_equal(proj.sum(), 9 / np.abs(affine[axis, axis]))
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((40, 40, 40, 2))
```

### Step 3: Assign unknown = 1

```python
data[20, 20, 20] = 1
```

### Step 4: Assign data_img = Nifti1Image(...)

```python
data_img = Nifti1Image(data, affine)
```

### Step 5: Assign mask = np.ones(...)

```python
mask = np.ones((40, 40, 40))
```

### Step 6: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask, affine)
```

### Step 7: Assign filenames = write_imgs_to_path(...)

```python
filenames = write_imgs_to_path(data_img, mask_img, file_path=tmp_path, create_files=create_files)
```

### Step 8: Assign series = apply_mask(...)

```python
series = apply_mask(filenames[0], filenames[1], smoothing_fwhm=9)
```

### Step 9: Assign series = np.reshape(...)

```python
series = np.reshape(series[0, :], (40, 40, 40))
```

### Step 10: Assign vmax = series.max(...)

```python
vmax = series.max()
```

### Step 11: Assign above_half_max = value

```python
above_half_max = series > 0.5 * vmax
```

### Step 12: Assign proj = np.any(...)

```python
proj = np.any(np.any(np.rollaxis(above_half_max, axis=axis), axis=-1), axis=-1)
```

### Step 13: Call assert_equal()

```python
assert_equal(proj.sum(), 9 / np.abs(affine[axis, axis]))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, create_files, affine

# Workflow
'Test smoothing of timeseries extraction.'
data = np.zeros((40, 40, 40, 2))
data[20, 20, 20] = 1
data_img = Nifti1Image(data, affine)
mask = np.ones((40, 40, 40))
mask_img = Nifti1Image(mask, affine)
filenames = write_imgs_to_path(data_img, mask_img, file_path=tmp_path, create_files=create_files)
series = apply_mask(filenames[0], filenames[1], smoothing_fwhm=9)
series = np.reshape(series[0, :], (40, 40, 40))
vmax = series.max()
above_half_max = series > 0.5 * vmax
for axis in (0, 1, 2):
    proj = np.any(np.any(np.rollaxis(above_half_max, axis=axis), axis=-1), axis=-1)
    assert_equal(proj.sum(), 9 / np.abs(affine[axis, axis]))
```

## Next Steps


---

*Source: test_masking.py:344 | Complexity: Advanced | Last updated: 2026-05-18*