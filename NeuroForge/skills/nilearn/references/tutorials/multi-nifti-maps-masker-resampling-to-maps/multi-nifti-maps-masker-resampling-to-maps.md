# How To: Multi Nifti Maps Masker Resampling To Maps

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test resampling to maps in MultiNiftiMapsMasker.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.testing`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: shape_mask, affine_eye, length, n_regions, shape_3d_large, img_fmri
```

## Step-by-Step Guide

### Step 1: 'Test resampling to maps in MultiNiftiMapsMasker.'

```python
'Test resampling to maps in MultiNiftiMapsMasker.'
```

**Verification:**
```python
assert_almost_equal(masker.maps_img_.affine, maps33_img.affine)
```

### Step 2: Assign unknown = generate_fake_fmri(...)

```python
_, mask22_img = generate_fake_fmri(shape_mask, affine=affine_eye, length=length)
```

**Verification:**
```python
assert masker.maps_img_.shape == maps33_img.shape
```

### Step 3: Assign unknown = generate_maps(...)

```python
maps33_img, _ = generate_maps(shape_3d_large, n_regions, affine=affine_eye)
```

**Verification:**
```python
assert_almost_equal(masker.mask_img_.affine, masker.maps_img_.affine)
```

### Step 4: Assign masker = MultiNiftiMapsMasker(...)

```python
masker = MultiNiftiMapsMasker(maps33_img, mask_img=mask22_img, resampling_target='maps', keep_masked_maps=True, standardize=None)
```

**Verification:**
```python
assert masker.mask_img_.shape == masker.maps_img_.shape[:3]
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(masker.maps_img_.affine, maps33_img.affine)
```

**Verification:**
```python
assert t.shape == (length, n_regions)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(masker.mask_img_.affine, masker.maps_img_.affine)
```

**Verification:**
```python
assert_almost_equal(fmri11_img_r.affine, masker.maps_img_.affine)
```

### Step 7: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform([img_fmri, img_fmri])
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.maps_img_.shape[:3], length)
```

### Step 8: Assign fmri11_img_r = masker.inverse_transform(...)

```python
fmri11_img_r = masker.inverse_transform(t)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(fmri11_img_r.affine, masker.maps_img_.affine)
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.maps_img_.shape[:3], length)
```


## Complete Example

```python
# Setup
# Fixtures: shape_mask, affine_eye, length, n_regions, shape_3d_large, img_fmri

# Workflow
'Test resampling to maps in MultiNiftiMapsMasker.'
_, mask22_img = generate_fake_fmri(shape_mask, affine=affine_eye, length=length)
maps33_img, _ = generate_maps(shape_3d_large, n_regions, affine=affine_eye)
masker = MultiNiftiMapsMasker(maps33_img, mask_img=mask22_img, resampling_target='maps', keep_masked_maps=True, standardize=None)
with pytest.warns(FutureWarning, match='"keep_masked_maps" parameter will be removed'):
    signals = masker.fit_transform([img_fmri, img_fmri])
assert_almost_equal(masker.maps_img_.affine, maps33_img.affine)
assert masker.maps_img_.shape == maps33_img.shape
assert_almost_equal(masker.mask_img_.affine, masker.maps_img_.affine)
assert masker.mask_img_.shape == masker.maps_img_.shape[:3]
for t in signals:
    assert t.shape == (length, n_regions)
    fmri11_img_r = masker.inverse_transform(t)
    assert_almost_equal(fmri11_img_r.affine, masker.maps_img_.affine)
    assert fmri11_img_r.shape == (*masker.maps_img_.shape[:3], length)
```

## Next Steps


---

*Source: test_multi_nifti_maps_masker.py:302 | Complexity: Advanced | Last updated: 2026-05-18*