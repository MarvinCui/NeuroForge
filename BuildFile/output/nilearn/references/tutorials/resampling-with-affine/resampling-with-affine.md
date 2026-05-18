# How To: Resampling With Affine

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test resampling with a given rotation part of the affine.

Check on 3D and 4D data.

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
# Fixtures: data, affine_eye, angle, force_resample
```

## Step-by-Step Guide

### Step 1: 'Test resampling with a given rotation part of the affine.\n\n    Check on 3D and 4D data.\n    '

```python
'Test resampling with a given rotation part of the affine.\n\n    Check on 3D and 4D data.\n    '
```

**Verification:**
```python
assert np.max(data) == np.max(get_data(rot_img))
```

### Step 2: Assign rot = rotation(...)

```python
rot = rotation(0, angle)
```

**Verification:**
```python
assert get_data(rot_img).dtype == data.dtype
```

### Step 3: Assign rot_img = resample_img(...)

```python
rot_img = resample_img(Nifti1Image(data, affine_eye), target_affine=rot, interpolation='nearest', force_resample=force_resample)
```

**Verification:**
```python
assert np.max(data) == np.max(get_data(rot_img))
```

### Step 4: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data.astype('>f8'), affine_eye)
```

### Step 5: Assign rot = rotation(...)

```python
rot = rotation(0, angle)
```

### Step 6: Assign rot_img = resample_img(...)

```python
rot_img = resample_img(img, target_affine=rot, interpolation='nearest', force_resample=force_resample)
```

**Verification:**
```python
assert np.max(data) == np.max(get_data(rot_img))
```


## Complete Example

```python
# Setup
# Fixtures: data, affine_eye, angle, force_resample

# Workflow
'Test resampling with a given rotation part of the affine.\n\n    Check on 3D and 4D data.\n    '
rot = rotation(0, angle)
rot_img = resample_img(Nifti1Image(data, affine_eye), target_affine=rot, interpolation='nearest', force_resample=force_resample)
assert np.max(data) == np.max(get_data(rot_img))
assert get_data(rot_img).dtype == data.dtype
img = Nifti1Image(data.astype('>f8'), affine_eye)
rot = rotation(0, angle)
rot_img = resample_img(img, target_affine=rot, interpolation='nearest', force_resample=force_resample)
assert np.max(data) == np.max(get_data(rot_img))
```

## Next Steps


---

*Source: test_resampling.py:256 | Complexity: Intermediate | Last updated: 2026-05-18*