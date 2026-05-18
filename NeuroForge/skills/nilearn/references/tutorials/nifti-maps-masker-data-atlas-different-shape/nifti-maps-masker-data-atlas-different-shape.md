# How To: Nifti Maps Masker Data Atlas Different Shape

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test with data and atlas of different shape.

The atlas should be resampled to the data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.testing`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: length, affine_eye, img_maps
```

## Step-by-Step Guide

### Step 1: 'Test with data and atlas of different shape.\n\n    The atlas should be resampled to the data.\n    '

```python
'Test with data and atlas of different shape.\n\n    The atlas should be resampled to the data.\n    '
```

**Verification:**
```python
assert all(('consider using nearest interpolation instead' not in x.message for x in warning_list))
```

### Step 2: Assign shape2 = value

```python
shape2 = (12, 10, 14)
```

**Verification:**
```python
assert_array_equal(masker.maps_img_.affine, affine2)
```

### Step 3: Assign shape22 = value

```python
shape22 = (5, 5, 6)
```

### Step 4: Assign affine2 = value

```python
affine2 = 2 * affine_eye
```

### Step 5: Assign unknown = 1

```python
affine2[-1, -1] = 1
```

### Step 6: Assign unknown = generate_fake_fmri(...)

```python
_, mask21_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
```

### Step 7: Assign unknown = generate_fake_fmri(...)

```python
fmri22_img, _ = generate_fake_fmri(shape22, affine=affine2, length=length)
```

### Step 8: Assign masker = NiftiMapsMasker(...)

```python
masker = NiftiMapsMasker(img_maps, mask_img=mask21_img, standardize=None)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(masker.maps_img_.affine, affine2)
```

### Step 10: Call masker.fit()

```python
masker.fit(fmri22_img)
```

**Verification:**
```python
assert all(('consider using nearest interpolation instead' not in x.message for x in warning_list))
```


## Complete Example

```python
# Setup
# Fixtures: length, affine_eye, img_maps

# Workflow
'Test with data and atlas of different shape.\n\n    The atlas should be resampled to the data.\n    '
shape2 = (12, 10, 14)
shape22 = (5, 5, 6)
affine2 = 2 * affine_eye
affine2[-1, -1] = 1
_, mask21_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
fmri22_img, _ = generate_fake_fmri(shape22, affine=affine2, length=length)
masker = NiftiMapsMasker(img_maps, mask_img=mask21_img, standardize=None)
with warnings.catch_warnings(record=True) as warning_list:
    masker.fit(fmri22_img)
    assert all(('consider using nearest interpolation instead' not in x.message for x in warning_list))
assert_array_equal(masker.maps_img_.affine, affine2)
```

## Next Steps


---

*Source: test_nifti_maps_masker.py:80 | Complexity: Advanced | Last updated: 2026-05-18*