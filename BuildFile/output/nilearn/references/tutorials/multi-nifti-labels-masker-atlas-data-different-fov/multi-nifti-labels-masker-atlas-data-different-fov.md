# How To: Multi Nifti Labels Masker Atlas Data Different Fov

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test with data and atlas of different shape.

The atlas should be resampled to the data.

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
# Fixtures: affine_eye, img_labels, length
```

## Step-by-Step Guide

### Step 1: 'Test with data and atlas of different shape.\n\n    The atlas should be resampled to the data.\n    '

```python
'Test with data and atlas of different shape.\n\n    The atlas should be resampled to the data.\n    '
```

**Verification:**
```python
assert_array_equal(masker.labels_img_.affine, affine2)
```

### Step 2: Assign shape2 = value

```python
shape2 = (8, 9, 10)
```

### Step 3: Assign shape22 = value

```python
shape22 = (5, 5, 6)
```

### Step 4: Assign affine2 = value

```python
affine2 = 2 * np.eye(4)
```

### Step 5: Assign unknown = 1

```python
affine2[-1, -1] = 1
```

### Step 6: Assign unknown = generate_fake_fmri(...)

```python
_, mask22_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
```

### Step 7: Assign unknown = generate_fake_fmri(...)

```python
fmri22_img, _ = generate_fake_fmri(shape22, affine=affine2, length=length)
```

### Step 8: Assign masker = MultiNiftiLabelsMasker(...)

```python
masker = MultiNiftiLabelsMasker(img_labels, mask_img=mask22_img, standardize=None)
```

### Step 9: Call masker.fit_transform()

```python
masker.fit_transform(fmri22_img)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(masker.labels_img_.affine, affine2)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, img_labels, length

# Workflow
'Test with data and atlas of different shape.\n\n    The atlas should be resampled to the data.\n    '
shape2 = (8, 9, 10)
shape22 = (5, 5, 6)
affine2 = 2 * np.eye(4)
affine2[-1, -1] = 1
_, mask22_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
fmri22_img, _ = generate_fake_fmri(shape22, affine=affine2, length=length)
masker = MultiNiftiLabelsMasker(img_labels, mask_img=mask22_img, standardize=None)
masker.fit_transform(fmri22_img)
assert_array_equal(masker.labels_img_.affine, affine2)
```

## Next Steps


---

*Source: test_multi_nifti_labels_masker.py:350 | Complexity: Advanced | Last updated: 2026-05-18*