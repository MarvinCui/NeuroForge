# How To: Filter And Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test filter_and_mask returns output with correct shape.

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

### Step 1: 'Test filter_and_mask returns output with correct shape.'

```python
'Test filter_and_mask returns output with correct shape.'
```

**Verification:**
```python
assert data.shape == (data_shape[3], np.prod(np.array(mask.shape)))
```

### Step 2: Assign data_shape = value

```python
data_shape = (20, 30, 40, 5)
```

### Step 3: Assign mask_shape = value

```python
mask_shape = (20, 30, 40)
```

### Step 4: Assign data = np.zeros(...)

```python
data = np.zeros(data_shape)
```

### Step 5: Assign mask = np.ones(...)

```python
mask = np.ones(mask_shape)
```

### Step 6: Assign data_img = Nifti1Image(...)

```python
data_img = Nifti1Image(data, affine_eye)
```

### Step 7: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask, affine_eye)
```

### Step 8: Assign params = NiftiMasker.get_params(...)

```python
params = NiftiMasker(standardize=None).get_params()
```

### Step 9: Assign unknown = value

```python
params['clean_kwargs'] = {}
```

### Step 10: Assign data = filter_and_mask(...)

```python
data = filter_and_mask(data_img, mask_img, params)
```

**Verification:**
```python
assert data.shape == (data_shape[3], np.prod(np.array(mask.shape)))
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Test filter_and_mask returns output with correct shape.'
data_shape = (20, 30, 40, 5)
mask_shape = (20, 30, 40)
data = np.zeros(data_shape)
mask = np.ones(mask_shape)
data_img = Nifti1Image(data, affine_eye)
mask_img = Nifti1Image(mask, affine_eye)
params = NiftiMasker(standardize=None).get_params()
params['clean_kwargs'] = {}
data = filter_and_mask(data_img, mask_img, params)
assert data.shape == (data_shape[3], np.prod(np.array(mask.shape)))
```

## Next Steps


---

*Source: test_nifti_masker.py:459 | Complexity: Advanced | Last updated: 2026-05-18*