# How To: Multi Nifti Labels Masker Resampling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test resampling in MultiNiftiLabelsMasker.

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
# Fixtures: affine_eye, n_regions, length, img_labels
```

## Step-by-Step Guide

### Step 1: 'Test resampling in MultiNiftiLabelsMasker.'

```python
'Test resampling in MultiNiftiLabelsMasker.'
```

**Verification:**
```python
assert_almost_equal(masker.labels_img_.affine, img_labels.affine)
```

### Step 2: Assign shape1 = value

```python
shape1 = (10, 11, 12)
```

**Verification:**
```python
assert masker.labels_img_.shape == img_labels.shape
```

### Step 3: Assign shape2 = value

```python
shape2 = (16, 17, 18)
```

**Verification:**
```python
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
```

### Step 4: Assign unknown = generate_fake_fmri(...)

```python
fmri11_img, _ = generate_fake_fmri(shape1, affine=affine_eye, length=length)
```

**Verification:**
```python
assert masker.mask_img_.shape == masker.labels_img_.shape[:3]
```

### Step 5: Assign unknown = generate_fake_fmri(...)

```python
_, mask22_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
```

**Verification:**
```python
assert t.shape == (length, n_regions)
```

### Step 6: Assign masker = MultiNiftiLabelsMasker(...)

```python
masker = MultiNiftiLabelsMasker(img_labels, mask_img=mask22_img, resampling_target='labels', keep_masked_labels=True, standardize=None)
```

**Verification:**
```python
assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
```

### Step 7: Assign fmri11_img = value

```python
fmri11_img = [fmri11_img, fmri11_img]
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(masker.labels_img_.affine, img_labels.affine)
```

**Verification:**
```python
assert masker.labels_img_.shape == img_labels.shape
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
```

**Verification:**
```python
assert masker.mask_img_.shape == masker.labels_img_.shape[:3]
```

### Step 10: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri11_img)
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
assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, n_regions, length, img_labels

# Workflow
'Test resampling in MultiNiftiLabelsMasker.'
shape1 = (10, 11, 12)
shape2 = (16, 17, 18)
fmri11_img, _ = generate_fake_fmri(shape1, affine=affine_eye, length=length)
_, mask22_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
masker = MultiNiftiLabelsMasker(img_labels, mask_img=mask22_img, resampling_target='labels', keep_masked_labels=True, standardize=None)
fmri11_img = [fmri11_img, fmri11_img]
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    signals = masker.fit_transform(fmri11_img)
assert_almost_equal(masker.labels_img_.affine, img_labels.affine)
assert masker.labels_img_.shape == img_labels.shape
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
assert masker.mask_img_.shape == masker.labels_img_.shape[:3]
for t in signals:
    assert t.shape == (length, n_regions)
    fmri11_img_r = masker.inverse_transform(t)
    assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
    assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```

## Next Steps


---

*Source: test_multi_nifti_labels_masker.py:251 | Complexity: Advanced | Last updated: 2026-05-18*