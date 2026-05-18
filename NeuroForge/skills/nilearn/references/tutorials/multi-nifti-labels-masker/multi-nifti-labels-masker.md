# How To: Multi Nifti Labels Masker

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check working of shape/affine checks.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: affine_eye, n_regions, shape_3d_default, length, img_labels
```

## Step-by-Step Guide

### Step 1: 'Check working of shape/affine checks.'

```python
'Check working of shape/affine checks.'
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
assert signals11.shape == (length, n_regions)
```

### Step 3: Assign masker11 = MultiNiftiLabelsMasker(...)

```python
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 4: Assign signals11 = masker11.fit_transform(...)

```python
signals11 = masker11.fit_transform(fmri11_img)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 5: Assign masker11 = MultiNiftiLabelsMasker(...)

```python
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
```

**Verification:**
```python
assert fmri11_img_r.shape == fmri11_img.shape
```

### Step 6: Call masker11.fit()

```python
masker11.fit()
```

**Verification:**
```python
assert_almost_equal(fmri11_img_r.affine, fmri11_img.affine)
```

### Step 7: Call masker11.inverse_transform()

```python
masker11.inverse_transform(signals11)
```

### Step 8: Assign masker11 = MultiNiftiLabelsMasker(...)

```python
masker11 = MultiNiftiLabelsMasker(img_labels, mask_img=mask11_img, resampling_target=None, keep_masked_labels=True, standardize=None)
```

**Verification:**
```python
assert signals11.shape == (length, n_regions)
```

### Step 9: Assign signals_input = value

```python
signals_input = [fmri11_img, fmri11_img]
```

### Step 10: Assign masker11 = MultiNiftiLabelsMasker(...)

```python
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
```

### Step 11: Assign signals11_list = masker11.fit_transform(...)

```python
signals11_list = masker11.fit_transform(signals_input)
```

### Step 12: Assign signals11 = masker11.fit_transform(...)

```python
signals11 = masker11.fit_transform(fmri11_img)
```

### Step 13: Assign signals11_list = masker11.fit_transform(...)

```python
signals11_list = masker11.fit_transform(signals_input)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 14: Assign fmri11_img_r = masker11.inverse_transform(...)

```python
fmri11_img_r = masker11.inverse_transform(signals)
```

**Verification:**
```python
assert fmri11_img_r.shape == fmri11_img.shape
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(fmri11_img_r.affine, fmri11_img.affine)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, n_regions, shape_3d_default, length, img_labels

# Workflow
'Check working of shape/affine checks.'
fmri11_img, mask11_img = generate_fake_fmri(shape_3d_default, affine=affine_eye, length=length)
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
signals11 = masker11.fit_transform(fmri11_img)
assert signals11.shape == (length, n_regions)
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
masker11.fit()
masker11.inverse_transform(signals11)
masker11 = MultiNiftiLabelsMasker(img_labels, mask_img=mask11_img, resampling_target=None, keep_masked_labels=True, standardize=None)
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    signals11 = masker11.fit_transform(fmri11_img)
assert signals11.shape == (length, n_regions)
signals_input = [fmri11_img, fmri11_img]
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    signals11_list = masker11.fit_transform(signals_input)
for signals in signals11_list:
    assert signals.shape == (length, n_regions)
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
signals11_list = masker11.fit_transform(signals_input)
for signals in signals11_list:
    assert signals.shape == (length, n_regions)
for signals in signals11_list:
    fmri11_img_r = masker11.inverse_transform(signals)
    assert fmri11_img_r.shape == fmri11_img.shape
    assert_almost_equal(fmri11_img_r.affine, fmri11_img.affine)
```

## Next Steps


---

*Source: test_multi_nifti_labels_masker.py:72 | Complexity: Advanced | Last updated: 2026-05-18*