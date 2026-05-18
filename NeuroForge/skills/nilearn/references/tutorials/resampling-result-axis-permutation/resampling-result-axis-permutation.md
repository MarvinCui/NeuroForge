# How To: Resampling Result Axis Permutation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Transform real data using easily checkable transformations.

For now: axis permutations
create a cuboid full of deterministic data, padded with one
voxel thickness of zeros

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
# Fixtures: affine_eye, axis_permutation, force_resample
```

## Step-by-Step Guide

### Step 1: 'Transform real data using easily checkable transformations.\n\n    For now: axis permutations\n    create a cuboid full of deterministic data, padded with one\n    voxel thickness of zeros\n    '

```python
'Transform real data using easily checkable transformations.\n\n    For now: axis permutations\n    create a cuboid full of deterministic data, padded with one\n    voxel thickness of zeros\n    '
```

**Verification:**
```python
assert_array_almost_equal(resampled_data, expected_data)
```

### Step 2: Assign core_shape = value

```python
core_shape = (3, 5, 4)
```

**Verification:**
```python
assert_array_almost_equal(resampled_data, expected_data)
```

### Step 3: Assign core_data = np.arange.reshape(...)

```python
core_data = np.arange(np.prod(core_shape)).reshape(core_shape)
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

### Step 8: Assign target_affine = value

```python
target_affine = np.eye(3)[axis_permutation]
```

### Step 9: Assign resampled_img = resample_img(...)

```python
resampled_img = resample_img(source_img, target_affine=target_affine, force_resample=force_resample)
```

### Step 10: Assign resampled_data = get_data(...)

```python
resampled_data = get_data(resampled_img)
```

### Step 11: Assign expected_data = full_data.transpose(...)

```python
expected_data = full_data.transpose(axis_permutation)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(resampled_data, expected_data)
```

### Step 13: Assign offset = np.array(...)

```python
offset = np.array([-2, 1, -3])
```

### Step 14: Assign target_affine = affine_eye

```python
target_affine = affine_eye
```

### Step 15: Assign unknown = value

```python
target_affine[:3, :3] = np.eye(3)[axis_permutation]
```

### Step 16: Assign unknown = offset

```python
target_affine[:3, 3] = offset
```

### Step 17: Assign resampled_img = resample_img(...)

```python
resampled_img = resample_img(source_img, target_affine=target_affine, force_resample=force_resample)
```

### Step 18: Assign resampled_data = get_data(...)

```python
resampled_data = get_data(resampled_img)
```

### Step 19: Assign offset_cropping = np.vstack.T.ravel.astype(...)

```python
offset_cropping = np.vstack([-offset[axis_permutation][np.newaxis, :], np.zeros([1, 3])]).T.ravel().astype(int)
```

### Step 20: Assign expected_data = pad_array(...)

```python
expected_data = pad_array(full_data.transpose(axis_permutation), list(offset_cropping))
```

### Step 21: Call assert_array_almost_equal()

```python
assert_array_almost_equal(resampled_data, expected_data)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, axis_permutation, force_resample

# Workflow
'Transform real data using easily checkable transformations.\n\n    For now: axis permutations\n    create a cuboid full of deterministic data, padded with one\n    voxel thickness of zeros\n    '
core_shape = (3, 5, 4)
core_data = np.arange(np.prod(core_shape)).reshape(core_shape)
full_data_shape = np.array(core_shape) + 2
full_data = np.zeros(full_data_shape)
full_data[tuple((slice(1, 1 + s) for s in core_shape))] = core_data
source_img = Nifti1Image(full_data, affine_eye)
target_affine = np.eye(3)[axis_permutation]
resampled_img = resample_img(source_img, target_affine=target_affine, force_resample=force_resample)
resampled_data = get_data(resampled_img)
expected_data = full_data.transpose(axis_permutation)
assert_array_almost_equal(resampled_data, expected_data)
offset = np.array([-2, 1, -3])
target_affine = affine_eye
target_affine[:3, :3] = np.eye(3)[axis_permutation]
target_affine[:3, 3] = offset
resampled_img = resample_img(source_img, target_affine=target_affine, force_resample=force_resample)
resampled_data = get_data(resampled_img)
offset_cropping = np.vstack([-offset[axis_permutation][np.newaxis, :], np.zeros([1, 3])]).T.ravel().astype(int)
expected_data = pad_array(full_data.transpose(axis_permutation), list(offset_cropping))
assert_array_almost_equal(resampled_data, expected_data)
```

## Next Steps


---

*Source: test_resampling.py:649 | Complexity: Advanced | Last updated: 2026-05-18*