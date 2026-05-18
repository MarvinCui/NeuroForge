# How To: Resample To Mask Warning

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that a warning is raised when data is        being resampled to mask's resolution.
    

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
# Fixtures: img_3d_rand_eye, affine_eye
```

## Step-by-Step Guide

### Step 1: "Check that a warning is raised when data is        being resampled to mask's resolution.\n    "

```python
"Check that a warning is raised when data is        being resampled to mask's resolution.\n    "
```

### Step 2: Assign mask = np.zeros(...)

```python
mask = np.zeros((12, 12, 12))
```

### Step 3: Assign unknown = 10

```python
mask[3:-3, 3:-3, 3:-3] = 10
```

### Step 4: Assign mask = mask.astype(...)

```python
mask = mask.astype('uint8')
```

### Step 5: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask, affine_eye)
```

### Step 6: Assign masker = NiftiMasker(...)

```python
masker = NiftiMasker(mask_img=mask_img, standardize=None)
```

### Step 7: Call masker.fit_transform()

```python
masker.fit_transform(img_3d_rand_eye)
```


## Complete Example

```python
# Setup
# Fixtures: img_3d_rand_eye, affine_eye

# Workflow
"Check that a warning is raised when data is        being resampled to mask's resolution.\n    "
mask = np.zeros((12, 12, 12))
mask[3:-3, 3:-3, 3:-3] = 10
mask = mask.astype('uint8')
mask_img = Nifti1Image(mask, affine_eye)
masker = NiftiMasker(mask_img=mask_img, standardize=None)
with pytest.warns(UserWarning, match='imgs are being resampled to the mask_img resolution. This process is memory intensive. You might want to provide a target_affine that is equal to the affine of the imgs or resample the mask beforehand to save memory and computation time.'):
    masker.fit_transform(img_3d_rand_eye)
```

## Next Steps


---

*Source: test_nifti_masker.py:134 | Complexity: Intermediate | Last updated: 2026-05-18*