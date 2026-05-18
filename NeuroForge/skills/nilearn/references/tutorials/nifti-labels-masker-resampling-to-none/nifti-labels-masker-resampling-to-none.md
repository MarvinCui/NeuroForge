# How To: Nifti Labels Masker Resampling To None

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test resampling to None in NiftiLabelsMasker.

All inputs must have same affine to avoid errors.

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
# Fixtures: affine_eye, length, shape_3d_default, img_labels
```

## Step-by-Step Guide

### Step 1: 'Test resampling to None in NiftiLabelsMasker.\n\n    All inputs must have same affine to avoid errors.\n    '

```python
'Test resampling to None in NiftiLabelsMasker.\n\n    All inputs must have same affine to avoid errors.\n    '
```

### Step 2: Assign unknown = generate_random_img(...)

```python
fmri_img, mask_img = generate_random_img(shape=(*shape_3d_default, length), affine=affine_eye)
```

### Step 3: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(img_labels, mask_img=mask_img, resampling_target=None, standardize=None)
```

### Step 4: Call masker.fit_transform()

```python
masker.fit_transform(fmri_img)
```

### Step 5: Assign unknown = generate_random_img(...)

```python
fmri_img, _ = generate_random_img((*shape_3d_default, length), affine=affine_eye * 2)
```

### Step 6: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(img_labels, mask_img=mask_img, resampling_target=None, standardize=None)
```

### Step 7: Call masker.fit_transform()

```python
masker.fit_transform(fmri_img)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, length, shape_3d_default, img_labels

# Workflow
'Test resampling to None in NiftiLabelsMasker.\n\n    All inputs must have same affine to avoid errors.\n    '
fmri_img, mask_img = generate_random_img(shape=(*shape_3d_default, length), affine=affine_eye)
masker = NiftiLabelsMasker(img_labels, mask_img=mask_img, resampling_target=None, standardize=None)
masker.fit_transform(fmri_img)
fmri_img, _ = generate_random_img((*shape_3d_default, length), affine=affine_eye * 2)
masker = NiftiLabelsMasker(img_labels, mask_img=mask_img, resampling_target=None, standardize=None)
with pytest.raises(ValueError, match='Following field of view errors were detected'):
    masker.fit_transform(fmri_img)
```

## Next Steps


---

*Source: test_nifti_labels_masker.py:498 | Complexity: Intermediate | Last updated: 2026-05-18*