# How To: Multi Nifti Labels Masker Resampling Clipped Labels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test with clipped labels.

Mask does not contain all labels.
Shapes do matter in that case,
because there is some resampling taking place.

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
# Fixtures: affine_eye, n_regions, length, img_labels, img_fmri
```

## Step-by-Step Guide

### Step 1: 'Test with clipped labels.\n\n    Mask does not contain all labels.\n    Shapes do matter in that case,\n    because there is some resampling taking place.\n    '

```python
'Test with clipped labels.\n\n    Mask does not contain all labels.\n    Shapes do matter in that case,\n    because there is some resampling taking place.\n    '
```

**Verification:**
```python
assert_almost_equal(masker.labels_img_.affine, img_labels.affine)
```

### Step 2: Assign shape2 = value

```python
shape2 = (8, 9, 10)
```

**Verification:**
```python
assert masker.labels_img_.shape == img_labels.shape
```

### Step 3: Assign unknown = generate_fake_fmri(...)

```python
_, mask22_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
```

**Verification:**
```python
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
```

### Step 4: Assign fmri11_img = value

```python
fmri11_img = [img_fmri, img_fmri]
```

**Verification:**
```python
assert masker.mask_img_.shape == masker.labels_img_.shape[:3]
```

### Step 5: Assign masker = MultiNiftiLabelsMasker(...)

```python
masker = MultiNiftiLabelsMasker(img_labels, mask_img=mask22_img, resampling_target='labels', keep_masked_labels=True, standardize=None)
```

**Verification:**
```python
assert uniq_labels[0] == 0
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(masker.labels_img_.affine, img_labels.affine)
```

**Verification:**
```python
assert len(uniq_labels) - 1 == n_regions
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
```

**Verification:**
```python
assert t.shape == (length, n_regions)
```

### Step 8: Assign uniq_labels = np.unique(...)

```python
uniq_labels = np.unique(get_data(masker.labels_img_))
```

**Verification:**
```python
assert (t.var(axis=0) == 0).sum() < n_regions
```

### Step 9: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri11_img)
```

**Verification:**
```python
assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
```

### Step 10: Assign fmri11_img_r = masker.inverse_transform(...)

```python
fmri11_img_r = masker.inverse_transform(t)
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, n_regions, length, img_labels, img_fmri

# Workflow
'Test with clipped labels.\n\n    Mask does not contain all labels.\n    Shapes do matter in that case,\n    because there is some resampling taking place.\n    '
shape2 = (8, 9, 10)
_, mask22_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
fmri11_img = [img_fmri, img_fmri]
masker = MultiNiftiLabelsMasker(img_labels, mask_img=mask22_img, resampling_target='labels', keep_masked_labels=True, standardize=None)
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    signals = masker.fit_transform(fmri11_img)
assert_almost_equal(masker.labels_img_.affine, img_labels.affine)
assert masker.labels_img_.shape == img_labels.shape
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
assert masker.mask_img_.shape == masker.labels_img_.shape[:3]
uniq_labels = np.unique(get_data(masker.labels_img_))
assert uniq_labels[0] == 0
assert len(uniq_labels) - 1 == n_regions
for t in signals:
    assert t.shape == (length, n_regions)
    assert (t.var(axis=0) == 0).sum() < n_regions
    fmri11_img_r = masker.inverse_transform(t)
    assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
    assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```

## Next Steps


---

*Source: test_multi_nifti_labels_masker.py:299 | Complexity: Advanced | Last updated: 2026-05-18*