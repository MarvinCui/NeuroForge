# How To: Filter And Mask Error

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check filter_and_mask fails if mask if 4D.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.maskers.nifti_masker`

**Setup Required:**
```python
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: 'Check filter_and_mask fails if mask if 4D.'

```python
'Check filter_and_mask fails if mask if 4D.'
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros([20, 30, 40, 5])
```

### Step 3: Assign mask = np.zeros(...)

```python
mask = np.zeros([20, 30, 40, 2])
```

### Step 4: Assign unknown = 1

```python
mask[10, 15, 20, :] = 1
```

### Step 5: Assign data_img = Nifti1Image(...)

```python
data_img = Nifti1Image(data, affine_eye)
```

### Step 6: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask, affine_eye)
```

### Step 7: Assign params = NiftiMasker.get_params(...)

```python
params = NiftiMasker().get_params()
```

### Step 8: Call filter_and_mask()

```python
filter_and_mask(data_img, mask_img, params)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Check filter_and_mask fails if mask if 4D.'
data = np.zeros([20, 30, 40, 5])
mask = np.zeros([20, 30, 40, 2])
mask[10, 15, 20, :] = 1
data_img = Nifti1Image(data, affine_eye)
mask_img = Nifti1Image(mask, affine_eye)
params = NiftiMasker().get_params()
with pytest.raises(DimensionError, match='Input data has incompatible dimensionality: Expected dimension is 3D and you provided a 4D image.'):
    filter_and_mask(data_img, mask_img, params)
```

## Next Steps


---

*Source: test_nifti_masker.py:437 | Complexity: Advanced | Last updated: 2026-05-18*