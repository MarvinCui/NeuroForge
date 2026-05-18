# How To: Is Nifti Spheres Masker Give Nans

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check behavior when data to fit_transform contains nan.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng, affine_eye
```

## Step-by-Step Guide

### Step 1: 'Check behavior when data to fit_transform contains nan.'

```python
'Check behavior when data to fit_transform contains nan.'
```

**Verification:**
```python
assert not np.isnan(np.sum(masker.fit_transform(img)))
```

### Step 2: Assign data_with_nans = np.zeros(...)

```python
data_with_nans = np.zeros((10, 10, 10), dtype=np.float32)
```

**Verification:**
```python
assert not np.isnan(np.sum(masker.fit_transform(img)))
```

### Step 3: Assign unknown = value

```python
data_with_nans[:, :, :] = np.nan
```

### Step 4: Assign data_without_nans = rng.random(...)

```python
data_without_nans = rng.random((9, 9, 9))
```

### Step 5: Assign indices = np.nonzero(...)

```python
indices = np.nonzero(data_without_nans)
```

### Step 6: Assign unknown = value

```python
data_with_nans[indices] = data_without_nans[indices]
```

### Step 7: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data_with_nans, affine_eye)
```

### Step 8: Assign seed = value

```python
seed = [(7, 7, 7)]
```

### Step 9: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker(seeds=seed, radius=2.0, standardize=None)
```

**Verification:**
```python
assert not np.isnan(np.sum(masker.fit_transform(img)))
```

### Step 10: Assign mask = np.ones(...)

```python
mask = np.ones((9, 9, 9))
```

### Step 11: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask, affine_eye)
```

### Step 12: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker(seeds=seed, radius=2.0, mask_img=mask_img, standardize=None)
```

**Verification:**
```python
assert not np.isnan(np.sum(masker.fit_transform(img)))
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye

# Workflow
'Check behavior when data to fit_transform contains nan.'
data_with_nans = np.zeros((10, 10, 10), dtype=np.float32)
data_with_nans[:, :, :] = np.nan
data_without_nans = rng.random((9, 9, 9))
indices = np.nonzero(data_without_nans)
data_with_nans[indices] = data_without_nans[indices]
img = Nifti1Image(data_with_nans, affine_eye)
seed = [(7, 7, 7)]
masker = NiftiSpheresMasker(seeds=seed, radius=2.0, standardize=None)
assert not np.isnan(np.sum(masker.fit_transform(img)))
mask = np.ones((9, 9, 9))
mask_img = Nifti1Image(mask, affine_eye)
masker = NiftiSpheresMasker(seeds=seed, radius=2.0, mask_img=mask_img, standardize=None)
assert not np.isnan(np.sum(masker.fit_transform(img)))
```

## Next Steps


---

*Source: test_nifti_spheres_masker.py:252 | Complexity: Advanced | Last updated: 2026-05-18*