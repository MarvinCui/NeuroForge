# How To: Resampling Nan

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that when the data has NaNs they do not propagate to the     whole image.
    

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `math`
- `os`
- `sys`
- `pathlib`
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.freesurfer`
- `numpy.testing`
- `nilearn._utils`
- `nilearn._utils.niimg`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.image.image`
- `nilearn.image.resampling`
- `nilearn.image.tests._testing`

**Setup Required:**
```python
# Fixtures: affine_eye, core_shape, force_resample
```

## Step-by-Step Guide

### Step 1: 'Test that when the data has NaNs they do not propagate to the     whole image.\n    '

```python
'Test that when the data has NaNs they do not propagate to the     whole image.\n    '
```

**Verification:**
```python
assert not np.all(non_nan)
```

### Step 2: Assign core_data = np.arange.reshape.astype(...)

```python
core_data = np.arange(np.prod(core_shape)).reshape(core_shape).astype(np.float64)
```

**Verification:**
```python
assert_array_almost_equal(resampled_data[non_nan], expected_data[non_nan])
```

### Step 3: Assign unknown = value

```python
core_data[2, 2:4, 1] = np.nan
```

**Verification:**
```python
assert not np.any(np.isfinite(resampled_data[np.logical_not(non_nan)]))
```

### Step 4: Assign full_data_shape = value

```python
full_data_shape = np.array(core_shape) + 2
```

### Step 5: Assign full_data = np.zeros(...)

```python
full_data = np.zeros(full_data_shape)
```

### Step 6: Assign unknown = core_data

```python
full_data[tuple((slice(1, 1 + s) for s in core_shape))] = core_data
```

### Step 7: Assign source_img = Nifti1Image(...)

```python
source_img = Nifti1Image(full_data, affine_eye)
```

### Step 8: Assign axis_permutation = value

```python
axis_permutation = [0, 1, 2]
```

### Step 9: Assign target_affine = value

```python
target_affine = np.eye(3)[axis_permutation]
```

### Step 10: Assign resampled_img = resample_img(...)

```python
resampled_img = resample_img(source_img, target_affine=target_affine, force_resample=force_resample)
```

### Step 11: Assign resampled_data = get_data(...)

```python
resampled_data = get_data(resampled_img)
```

### Step 12: Assign expected_data = full_data.transpose(...)

```python
expected_data = full_data.transpose(axis_permutation)
```

### Step 13: Assign non_nan = np.isfinite(...)

```python
non_nan = np.isfinite(expected_data)
```

**Verification:**
```python
assert not np.all(non_nan)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(resampled_data[non_nan], expected_data[non_nan])
```

**Verification:**
```python
assert not np.any(np.isfinite(resampled_data[np.logical_not(non_nan)]))
```

### Step 15: Call axis_permutation.append()

```python
axis_permutation.append(3)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, core_shape, force_resample

# Workflow
'Test that when the data has NaNs they do not propagate to the     whole image.\n    '
core_data = np.arange(np.prod(core_shape)).reshape(core_shape).astype(np.float64)
core_data[2, 2:4, 1] = np.nan
full_data_shape = np.array(core_shape) + 2
full_data = np.zeros(full_data_shape)
full_data[tuple((slice(1, 1 + s) for s in core_shape))] = core_data
source_img = Nifti1Image(full_data, affine_eye)
axis_permutation = [0, 1, 2]
target_affine = np.eye(3)[axis_permutation]
resampled_img = resample_img(source_img, target_affine=target_affine, force_resample=force_resample)
resampled_data = get_data(resampled_img)
if full_data.ndim == 4:
    axis_permutation.append(3)
expected_data = full_data.transpose(axis_permutation)
non_nan = np.isfinite(expected_data)
assert not np.all(non_nan)
assert_array_almost_equal(resampled_data[non_nan], expected_data[non_nan])
assert not np.any(np.isfinite(resampled_data[np.logical_not(non_nan)]))
```

## Next Steps


---

*Source: test_resampling.py:702 | Complexity: Advanced | Last updated: 2026-05-18*