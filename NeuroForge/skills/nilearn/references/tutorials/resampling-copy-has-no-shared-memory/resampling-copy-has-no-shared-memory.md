# How To: Resampling Copy Has No Shared Memory

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: copy=true guarantees output array shares no memory with input array.

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
# Fixtures: target_shape, force_resample, data, affine_eye
```

## Step-by-Step Guide

### Step 1: 'copy=true guarantees output array shares no memory with input array.'

```python
'copy=true guarantees output array shares no memory with input array.'
```

**Verification:**
```python
assert img_r == img
```

### Step 2: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

**Verification:**
```python
assert not np.may_share_memory(get_data(img_r), get_data(img))
```

### Step 3: Assign target_affine = value

```python
target_affine = None if target_shape is None else affine_eye
```

**Verification:**
```python
assert_almost_equal(get_data(img_r), get_data(img))
```

### Step 4: Assign img_r = resample_img(...)

```python
img_r = resample_img(img, target_affine=target_affine, target_shape=target_shape, copy=False, force_resample=force_resample)
```

**Verification:**
```python
assert_almost_equal(img_r.affine, img.affine)
```

### Step 5: Assign img_r = resample_img(...)

```python
img_r = resample_img(img, target_affine=target_affine, target_shape=target_shape, copy=True, force_resample=force_resample)
```

**Verification:**
```python
assert not np.may_share_memory(get_data(img_r), get_data(img))
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(get_data(img_r), get_data(img))
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(img_r.affine, img.affine)
```


## Complete Example

```python
# Setup
# Fixtures: target_shape, force_resample, data, affine_eye

# Workflow
'copy=true guarantees output array shares no memory with input array.'
img = Nifti1Image(data, affine_eye)
target_affine = None if target_shape is None else affine_eye
img_r = resample_img(img, target_affine=target_affine, target_shape=target_shape, copy=False, force_resample=force_resample)
assert img_r == img
img_r = resample_img(img, target_affine=target_affine, target_shape=target_shape, copy=True, force_resample=force_resample)
assert not np.may_share_memory(get_data(img_r), get_data(img))
assert_almost_equal(get_data(img_r), get_data(img))
assert_almost_equal(img_r.affine, img.affine)
```

## Next Steps


---

*Source: test_resampling.py:376 | Complexity: Intermediate | Last updated: 2026-05-18*