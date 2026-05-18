# How To: Multi Nifti Maps Masker Resampling Clipped Mask

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test with clipped maps: mask does not contain all maps.

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
# Fixtures: affine_eye, length, n_regions, img_fmri
```

## Step-by-Step Guide

### Step 1: 'Test with clipped maps: mask does not contain all maps.'

```python
'Test with clipped maps: mask does not contain all maps.'
```

**Verification:**
```python
assert_almost_equal(masker.maps_img_.affine, maps33_img.affine)
```

### Step 2: Assign shape2 = value

```python
shape2 = (8, 9, 10)
```

**Verification:**
```python
assert masker.maps_img_.shape == maps33_img.shape
```

### Step 3: Assign shape3 = value

```python
shape3 = (16, 18, 20)
```

**Verification:**
```python
assert_almost_equal(masker.mask_img_.affine, masker.maps_img_.affine)
```

### Step 4: Assign affine2 = np.diag(...)

```python
affine2 = np.diag((2, 2, 2, 1))
```

**Verification:**
```python
assert masker.mask_img_.shape == masker.maps_img_.shape[:3]
```

### Step 5: Assign unknown = generate_fake_fmri(...)

```python
_, mask22_img = generate_fake_fmri(shape2, length=1, affine=affine2)
```

**Verification:**
```python
assert t.shape == (length, n_regions)
```

### Step 6: Assign unknown = generate_maps(...)

```python
maps33_img, _ = generate_maps(shape3, n_regions, affine=affine_eye)
```

**Verification:**
```python
assert (t.var(axis=0) == 0).sum() < n_regions
```

### Step 7: Assign masker = MultiNiftiMapsMasker(...)

```python
masker = MultiNiftiMapsMasker(maps33_img, mask_img=mask22_img, resampling_target='maps', keep_masked_maps=True, standardize=None)
```

**Verification:**
```python
assert_almost_equal(fmri11_img_r.affine, masker.maps_img_.affine)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(masker.maps_img_.affine, maps33_img.affine)
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.maps_img_.shape[:3], length)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(masker.mask_img_.affine, masker.maps_img_.affine)
```

**Verification:**
```python
assert masker.mask_img_.shape == masker.maps_img_.shape[:3]
```

### Step 10: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform([img_fmri, img_fmri])
```

**Verification:**
```python
assert t.shape == (length, n_regions)
```

### Step 11: Assign fmri11_img_r = masker.inverse_transform(...)

```python
fmri11_img_r = masker.inverse_transform(t)
```

### Step 12: Call assert_almost_equal()

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
# Fixtures: affine_eye, length, n_regions, img_fmri

# Workflow
'Test with clipped maps: mask does not contain all maps.'
shape2 = (8, 9, 10)
shape3 = (16, 18, 20)
affine2 = np.diag((2, 2, 2, 1))
_, mask22_img = generate_fake_fmri(shape2, length=1, affine=affine2)
maps33_img, _ = generate_maps(shape3, n_regions, affine=affine_eye)
masker = MultiNiftiMapsMasker(maps33_img, mask_img=mask22_img, resampling_target='maps', keep_masked_maps=True, standardize=None)
with pytest.warns(FutureWarning, match='"keep_masked_maps" parameter will be removed'):
    signals = masker.fit_transform([img_fmri, img_fmri])
assert_almost_equal(masker.maps_img_.affine, maps33_img.affine)
assert masker.maps_img_.shape == maps33_img.shape
assert_almost_equal(masker.mask_img_.affine, masker.maps_img_.affine)
assert masker.mask_img_.shape == masker.maps_img_.shape[:3]
for t in signals:
    assert t.shape == (length, n_regions)
    assert (t.var(axis=0) == 0).sum() < n_regions
    fmri11_img_r = masker.inverse_transform(t)
    assert_almost_equal(fmri11_img_r.affine, masker.maps_img_.affine)
    assert fmri11_img_r.shape == (*masker.maps_img_.shape[:3], length)
```

## Next Steps


---

*Source: test_multi_nifti_maps_masker.py:344 | Complexity: Advanced | Last updated: 2026-05-18*