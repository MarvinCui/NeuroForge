# How To: Resampling Fill Value

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test resampling with a non-zero fill value.

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
# Fixtures: data, affine_eye, value, force_resample
```

## Step-by-Step Guide

### Step 1: 'Test resampling with a non-zero fill value.\n\n    Check on 3D and 4D data.\n    '

```python
'Test resampling with a non-zero fill value.\n\n    Check on 3D and 4D data.\n    '
```

**Verification:**
```python
assert get_data(rot_img).flatten()[0] == value
```

### Step 2: Assign angle = value

```python
angle = np.pi / 4
```

**Verification:**
```python
assert get_data(rot_img2).flatten()[0] == value
```

### Step 3: Assign rot = rotation(...)

```python
rot = rotation(0, angle)
```

**Verification:**
```python
assert get_data(rot_img).flatten()[0] == value
```

### Step 4: Assign rot_img2 = resample_to_img(...)

```python
rot_img2 = resample_to_img(Nifti1Image(data, affine_eye), rot_img, interpolation='nearest', fill_value=value, force_resample=force_resample)
```

**Verification:**
```python
assert get_data(rot_img2).flatten()[0] == value
```

### Step 5: Assign rot_img = resample_img(...)

```python
rot_img = resample_img(Nifti1Image(data, affine_eye), target_affine=rot, interpolation='nearest', fill_value=value, clip=False, force_resample=force_resample)
```

### Step 6: Assign rot_img = resample_img(...)

```python
rot_img = resample_img(Nifti1Image(data, affine_eye), target_affine=rot, interpolation='nearest', clip=False, force_resample=force_resample)
```


## Complete Example

```python
# Setup
# Fixtures: data, affine_eye, value, force_resample

# Workflow
'Test resampling with a non-zero fill value.\n\n    Check on 3D and 4D data.\n    '
angle = np.pi / 4
rot = rotation(0, angle)
if value:
    rot_img = resample_img(Nifti1Image(data, affine_eye), target_affine=rot, interpolation='nearest', fill_value=value, clip=False, force_resample=force_resample)
else:
    rot_img = resample_img(Nifti1Image(data, affine_eye), target_affine=rot, interpolation='nearest', clip=False, force_resample=force_resample)
assert get_data(rot_img).flatten()[0] == value
rot_img2 = resample_to_img(Nifti1Image(data, affine_eye), rot_img, interpolation='nearest', fill_value=value, force_resample=force_resample)
assert get_data(rot_img2).flatten()[0] == value
```

## Next Steps


---

*Source: test_resampling.py:214 | Complexity: Intermediate | Last updated: 2026-05-18*