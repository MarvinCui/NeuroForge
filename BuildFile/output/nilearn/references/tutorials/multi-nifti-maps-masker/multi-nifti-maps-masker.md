# How To: Multi Nifti Maps Masker

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check basic functions of MultiNiftiMapsMasker.

- fit, transform, fit_transform, inverse_transform.
- 4D and list[4D] inputs

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
# Fixtures: affine_eye, length, n_regions, shape_3d_default, img_maps
```

## Step-by-Step Guide

### Step 1: 'Check basic functions of MultiNiftiMapsMasker.\n\n    - fit, transform, fit_transform, inverse_transform.\n    - 4D and list[4D] inputs\n    '

```python
'Check basic functions of MultiNiftiMapsMasker.\n\n    - fit, transform, fit_transform, inverse_transform.\n    - 4D and list[4D] inputs\n    '
```

**Verification:**
```python
assert signals11.shape == (length, n_regions)
```

### Step 2: Assign unknown = generate_fake_fmri(...)

```python
fmri11_img, mask11_img = generate_fake_fmri(shape_3d_default, affine=affine_eye, length=length)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 3: Assign masker = MultiNiftiMapsMasker(...)

```python
masker = MultiNiftiMapsMasker(img_maps, mask_img=mask11_img, resampling_target=None, keep_masked_maps=True, standardize=None)
```

**Verification:**
```python
assert fmri11_img_r.shape == fmri11_img.shape
```

### Step 4: Call MultiNiftiMapsMasker.fit_transform()

```python
MultiNiftiMapsMasker(img_maps, standardize=None).fit_transform(fmri11_img)
```

**Verification:**
```python
assert_almost_equal(fmri11_img_r.affine, fmri11_img.affine)
```

### Step 5: Assign signals_input = value

```python
signals_input = [fmri11_img, fmri11_img]
```

### Step 6: Assign masker = MultiNiftiMapsMasker(...)

```python
masker = MultiNiftiMapsMasker(img_maps, resampling_target=None, standardize=None)
```

### Step 7: Call masker.fit()

```python
masker.fit()
```

### Step 8: Call masker.inverse_transform()

```python
masker.inverse_transform(signals)
```

### Step 9: Assign signals11 = masker.fit_transform(...)

```python
signals11 = masker.fit_transform(fmri11_img)
```

### Step 10: Assign signals11_list = masker.fit_transform(...)

```python
signals11_list = masker.fit_transform(signals_input)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 11: Assign fmri11_img_r = masker.inverse_transform(...)

```python
fmri11_img_r = masker.inverse_transform(signals)
```

**Verification:**
```python
assert fmri11_img_r.shape == fmri11_img.shape
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(fmri11_img_r.affine, fmri11_img.affine)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, length, n_regions, shape_3d_default, img_maps

# Workflow
'Check basic functions of MultiNiftiMapsMasker.\n\n    - fit, transform, fit_transform, inverse_transform.\n    - 4D and list[4D] inputs\n    '
fmri11_img, mask11_img = generate_fake_fmri(shape_3d_default, affine=affine_eye, length=length)
masker = MultiNiftiMapsMasker(img_maps, mask_img=mask11_img, resampling_target=None, keep_masked_maps=True, standardize=None)
with pytest.warns(FutureWarning, match='"keep_masked_maps" parameter will be removed in version 0\\.15'):
    signals11 = masker.fit_transform(fmri11_img)
assert signals11.shape == (length, n_regions)
MultiNiftiMapsMasker(img_maps, standardize=None).fit_transform(fmri11_img)
signals_input = [fmri11_img, fmri11_img]
with pytest.warns(FutureWarning, match='"keep_masked_maps" parameter will be removed'):
    signals11_list = masker.fit_transform(signals_input)
for signals in signals11_list:
    assert signals.shape == (length, n_regions)
for signals in signals11_list:
    fmri11_img_r = masker.inverse_transform(signals)
    assert fmri11_img_r.shape == fmri11_img.shape
    assert_almost_equal(fmri11_img_r.affine, fmri11_img.affine)
masker = MultiNiftiMapsMasker(img_maps, resampling_target=None, standardize=None)
masker.fit()
masker.inverse_transform(signals)
```

## Next Steps


---

*Source: test_multi_nifti_maps_masker.py:72 | Complexity: Advanced | Last updated: 2026-05-18*