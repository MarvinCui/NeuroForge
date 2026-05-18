# How To: Nifti Labels Masker Resampling To Labels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test resampling to labels in NiftiLabelsMasker.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `numpy`
- `pandas`
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
# Fixtures: affine_eye, shape_3d_default, n_regions, length
```

## Step-by-Step Guide

### Step 1: 'Test resampling to labels in NiftiLabelsMasker.'

```python
'Test resampling to labels in NiftiLabelsMasker.'
```

**Verification:**
```python
assert_almost_equal(masker.labels_img_.affine, labels_img.affine)
```

### Step 2: Assign shape1 = value

```python
shape1 = (*shape_3d_default, length)
```

**Verification:**
```python
assert masker.labels_img_.shape == labels_img.shape
```

### Step 3: Assign shape2 = value

```python
shape2 = (16, 17, 18, length)
```

**Verification:**
```python
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
```

### Step 4: Assign shape3 = value

```python
shape3 = (13, 14, 15)
```

**Verification:**
```python
assert masker.mask_img_.shape == masker.labels_img_.shape[:3]
```

### Step 5: Assign unknown = generate_random_img(...)

```python
fmri_img, _ = generate_random_img(shape1, affine=affine_eye)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 6: Assign unknown = generate_random_img(...)

```python
_, mask_img = generate_random_img(shape2, affine=affine_eye)
```

**Verification:**
```python
assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
```

### Step 7: Assign labels_img = generate_labeled_regions(...)

```python
labels_img = generate_labeled_regions(shape3, n_regions, affine=affine_eye)
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```

### Step 8: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(labels_img, mask_img=mask_img, resampling_target='labels', standardize=None)
```

### Step 9: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri_img)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(masker.labels_img_.affine, labels_img.affine)
```

**Verification:**
```python
assert masker.labels_img_.shape == labels_img.shape
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
```

**Verification:**
```python
assert masker.mask_img_.shape == masker.labels_img_.shape[:3]
```

### Step 12: Assign fmri11_img_r = masker.inverse_transform(...)

```python
fmri11_img_r = masker.inverse_transform(signals)
```

### Step 13: Call assert_almost_equal()

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
# Fixtures: affine_eye, shape_3d_default, n_regions, length

# Workflow
'Test resampling to labels in NiftiLabelsMasker.'
shape1 = (*shape_3d_default, length)
shape2 = (16, 17, 18, length)
shape3 = (13, 14, 15)
fmri_img, _ = generate_random_img(shape1, affine=affine_eye)
_, mask_img = generate_random_img(shape2, affine=affine_eye)
labels_img = generate_labeled_regions(shape3, n_regions, affine=affine_eye)
masker = NiftiLabelsMasker(labels_img, mask_img=mask_img, resampling_target='labels', standardize=None)
signals = masker.fit_transform(fmri_img)
assert_almost_equal(masker.labels_img_.affine, labels_img.affine)
assert masker.labels_img_.shape == labels_img.shape
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
assert masker.mask_img_.shape == masker.labels_img_.shape[:3]
assert signals.shape == (length, n_regions)
fmri11_img_r = masker.inverse_transform(signals)
assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```

## Next Steps


---

*Source: test_nifti_labels_masker.py:397 | Complexity: Advanced | Last updated: 2026-05-18*