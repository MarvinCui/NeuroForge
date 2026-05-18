# How To: Nifti Labels Masker

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check working of shape/affine checks.

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
# Fixtures: affine_eye, shape_3d_default, n_regions, length, img_labels
```

## Step-by-Step Guide

### Step 1: 'Check working of shape/affine checks.'

```python
'Check working of shape/affine checks.'
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 2: Assign shape1 = value

```python
shape1 = (*shape_3d_default, length)
```

**Verification:**
```python
assert masker.n_elements_ == n_regions
```

### Step 3: Assign unknown = generate_random_img(...)

```python
fmri_img, mask11_img = generate_random_img(shape1, affine=affine_eye)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 4: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
```

**Verification:**
```python
assert signals.shape == (length, n_regions - 1)
```

### Step 5: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri_img)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 6: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
```

### Step 7: Call masker.fit()

```python
masker.fit()
```

**Verification:**
```python
assert masker.n_elements_ == n_regions
```

### Step 8: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri_img)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 9: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(img_labels, mask_img=mask11_img, resampling_target=None, standardize=None)
```

### Step 10: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri_img)
```

**Verification:**
```python
assert signals.shape == (length, n_regions - 1)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, shape_3d_default, n_regions, length, img_labels

# Workflow
'Check working of shape/affine checks.'
shape1 = (*shape_3d_default, length)
fmri_img, mask11_img = generate_random_img(shape1, affine=affine_eye)
masker = NiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
signals = masker.fit_transform(fmri_img)
assert signals.shape == (length, n_regions)
masker = NiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
masker.fit()
assert masker.n_elements_ == n_regions
signals = masker.fit_transform(fmri_img)
assert signals.shape == (length, n_regions)
masker = NiftiLabelsMasker(img_labels, mask_img=mask11_img, resampling_target=None, standardize=None)
signals = masker.fit_transform(fmri_img)
assert signals.shape == (length, n_regions - 1)
```

## Next Steps


---

*Source: test_nifti_labels_masker.py:76 | Complexity: Advanced | Last updated: 2026-05-18*