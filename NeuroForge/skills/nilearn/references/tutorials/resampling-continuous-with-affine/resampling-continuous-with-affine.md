# How To: Resampling Continuous With Affine

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test resampling continuous with affine

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

### Step 1: Assign rot = rotation(...)

```python
rot = rotation(0, angle)
```

**Verification:**
```python
assert_allclose(get_data(img)[mask], get_data(rot_img_back)[mask])
```

### Step 2: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

**Verification:**
```python
assert get_data(rot_img).dtype == np.dtype(data.dtype.name.replace('int', 'float'))
```

### Step 3: Assign rot_img = resample_img(...)

```python
rot_img = resample_img(img, target_affine=rot, interpolation='continuous', force_resample=force_resample)
```

### Step 4: Assign rot_img_back = resample_img(...)

```python
rot_img_back = resample_img(rot_img, target_affine=affine_eye, interpolation='continuous', force_resample=force_resample)
```

### Step 5: Assign center = slice(...)

```python
center = slice(1, 9)
```

### Step 6: Assign mask = value

```python
mask = (0, center, center)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(get_data(img)[mask], get_data(rot_img_back)[mask])
```

**Verification:**
```python
assert get_data(rot_img).dtype == np.dtype(data.dtype.name.replace('int', 'float'))
```


## Complete Example

```python
# Setup
# Fixtures: data, affine_eye, angle, force_resample

# Workflow
rot = rotation(0, angle)
img = Nifti1Image(data, affine_eye)
rot_img = resample_img(img, target_affine=rot, interpolation='continuous', force_resample=force_resample)
rot_img_back = resample_img(rot_img, target_affine=affine_eye, interpolation='continuous', force_resample=force_resample)
center = slice(1, 9)
mask = (0, center, center)
assert_allclose(get_data(img)[mask], get_data(rot_img_back)[mask])
assert get_data(rot_img).dtype == np.dtype(data.dtype.name.replace('int', 'float'))
```

## Next Steps


---

*Source: test_resampling.py:291 | Complexity: Intermediate | Last updated: 2026-05-18*