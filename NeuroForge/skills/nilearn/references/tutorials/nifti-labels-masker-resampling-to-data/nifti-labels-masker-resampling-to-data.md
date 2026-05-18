# How To: Nifti Labels Masker Resampling To Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test resampling to data in NiftiLabelsMasker.

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
# Fixtures: affine_eye, n_regions, length
```

## Step-by-Step Guide

### Step 1: 'Test resampling to data in NiftiLabelsMasker.'

```python
'Test resampling to data in NiftiLabelsMasker.'
```

**Verification:**
```python
assert_array_equal(masker.labels_img_.affine, affine2)
```

### Step 2: Assign shape2 = value

```python
shape2 = (8, 9, 10, length)
```

### Step 3: Assign shape3 = value

```python
shape3 = (16, 18, 20)
```

### Step 4: Assign unknown = generate_random_img(...)

```python
_, mask_img = generate_random_img(shape2, affine=affine_eye)
```

### Step 5: Assign labels_img = generate_labeled_regions(...)

```python
labels_img = generate_labeled_regions(shape3, n_regions, affine=affine_eye)
```

### Step 6: Assign shape22 = value

```python
shape22 = (5, 5, 6, length)
```

### Step 7: Assign affine2 = value

```python
affine2 = 2 * affine_eye
```

### Step 8: Assign unknown = 1

```python
affine2[-1, -1] = 1
```

### Step 9: Assign unknown = generate_random_img(...)

```python
fmri_img, _ = generate_random_img(shape22, affine=affine2)
```

### Step 10: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(labels_img, mask_img=mask_img, resampling_target='data', standardize=None)
```

### Step 11: Call masker.fit_transform()

```python
masker.fit_transform(fmri_img)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(masker.labels_img_.affine, affine2)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, n_regions, length

# Workflow
'Test resampling to data in NiftiLabelsMasker.'
shape2 = (8, 9, 10, length)
shape3 = (16, 18, 20)
_, mask_img = generate_random_img(shape2, affine=affine_eye)
labels_img = generate_labeled_regions(shape3, n_regions, affine=affine_eye)
shape22 = (5, 5, 6, length)
affine2 = 2 * affine_eye
affine2[-1, -1] = 1
fmri_img, _ = generate_random_img(shape22, affine=affine2)
masker = NiftiLabelsMasker(labels_img, mask_img=mask_img, resampling_target='data', standardize=None)
masker.fit_transform(fmri_img)
assert_array_equal(masker.labels_img_.affine, affine2)
```

## Next Steps


---

*Source: test_nifti_labels_masker.py:314 | Complexity: Advanced | Last updated: 2026-05-18*