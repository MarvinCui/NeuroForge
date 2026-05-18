# How To: Nifti Maps Masker Resampling To Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test resampling to_mask in NiftiMapsMasker.

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
# Fixtures: length, n_regions, affine_eye, shape_mask, shape_3d_large, img_fmri
```

## Step-by-Step Guide

### Step 1: 'Test resampling to_mask in NiftiMapsMasker.'

```python
'Test resampling to_mask in NiftiMapsMasker.'
```

**Verification:**
```python
assert all(('consider using nearest interpolation instead' not in str(x) for x in warning_list))
```

### Step 2: Assign unknown = generate_fake_fmri(...)

```python
_, mask22_img = generate_fake_fmri(shape_mask, length=length, affine=affine_eye)
```

**Verification:**
```python
assert_almost_equal(masker.mask_img_.affine, mask22_img.affine)
```

### Step 3: Assign unknown = generate_maps(...)

```python
maps33_img, _ = generate_maps(shape_3d_large, n_regions, affine=affine_eye)
```

**Verification:**
```python
assert masker.mask_img_.shape == mask22_img.shape
```

### Step 4: Assign masker = NiftiMapsMasker(...)

```python
masker = NiftiMapsMasker(maps33_img, mask_img=mask22_img, resampling_target='mask', keep_masked_maps=True, standardize=None)
```

**Verification:**
```python
assert_almost_equal(masker.maps_img_.affine, masker.mask_img_.affine)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(masker.mask_img_.affine, mask22_img.affine)
```

**Verification:**
```python
assert masker.maps_img_.shape[:3] == masker.mask_img_.shape
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(masker.maps_img_.affine, masker.mask_img_.affine)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 7: Assign fmri11_img_r = masker.inverse_transform(...)

```python
fmri11_img_r = masker.inverse_transform(signals)
```

**Verification:**
```python
assert_almost_equal(fmri11_img_r.affine, masker.mask_img_.affine)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(fmri11_img_r.affine, masker.mask_img_.affine)
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.mask_img_.shape[:3], length)
```

### Step 9: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(img_fmri)
```

**Verification:**
```python
assert all(('consider using nearest interpolation instead' not in str(x) for x in warning_list))
```


## Complete Example

```python
# Setup
# Fixtures: length, n_regions, affine_eye, shape_mask, shape_3d_large, img_fmri

# Workflow
'Test resampling to_mask in NiftiMapsMasker.'
_, mask22_img = generate_fake_fmri(shape_mask, length=length, affine=affine_eye)
maps33_img, _ = generate_maps(shape_3d_large, n_regions, affine=affine_eye)
masker = NiftiMapsMasker(maps33_img, mask_img=mask22_img, resampling_target='mask', keep_masked_maps=True, standardize=None)
with warnings.catch_warnings(record=True) as warning_list, pytest.warns(FutureWarning, match='"keep_masked_maps" parameter will be removed'):
    signals = masker.fit_transform(img_fmri)
    assert all(('consider using nearest interpolation instead' not in str(x) for x in warning_list))
assert_almost_equal(masker.mask_img_.affine, mask22_img.affine)
assert masker.mask_img_.shape == mask22_img.shape
assert_almost_equal(masker.maps_img_.affine, masker.mask_img_.affine)
assert masker.maps_img_.shape[:3] == masker.mask_img_.shape
assert signals.shape == (length, n_regions)
fmri11_img_r = masker.inverse_transform(signals)
assert_almost_equal(fmri11_img_r.affine, masker.mask_img_.affine)
assert fmri11_img_r.shape == (*masker.mask_img_.shape[:3], length)
```

## Next Steps


---

*Source: test_nifti_maps_masker.py:270 | Complexity: Advanced | Last updated: 2026-05-18*