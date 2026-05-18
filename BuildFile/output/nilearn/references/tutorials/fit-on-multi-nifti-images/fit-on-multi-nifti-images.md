# How To: Fit On Multi Nifti Images

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fit on multi nifti images

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.maskers`
- `nilearn.regions.parcellations`
- `nilearn.surface`
- `nilearn.surface.tests.test_surface`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`

**Setup Required:**
```python
# Fixtures: method, image_1, affine_eye
```

## Step-by-Step Guide

### Step 1: Assign fmri_imgs = value

```python
fmri_imgs = [image_1] * 3
```

**Verification:**
```python
assert parcellator.labels_img_ is not None
```

### Step 2: Assign parcellator = Parcellations(...)

```python
parcellator = Parcellations(method=method, n_parcels=5)
```

### Step 3: Call parcellator.fit()

```python
parcellator.fit(fmri_imgs)
```

**Verification:**
```python
assert parcellator.labels_img_ is not None
```

### Step 4: Assign mask_img = np.ones(...)

```python
mask_img = np.ones((10, 11, 12))
```

### Step 5: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask_img, affine_eye)
```

### Step 6: Assign parcellator = Parcellations(...)

```python
parcellator = Parcellations(method=method, n_parcels=5, mask=mask_img)
```

### Step 7: Call parcellator.fit()

```python
parcellator.fit(fmri_imgs)
```


## Complete Example

```python
# Setup
# Fixtures: method, image_1, affine_eye

# Workflow
fmri_imgs = [image_1] * 3
parcellator = Parcellations(method=method, n_parcels=5)
parcellator.fit(fmri_imgs)
assert parcellator.labels_img_ is not None
mask_img = np.ones((10, 11, 12))
mask_img = Nifti1Image(mask_img, affine_eye)
parcellator = Parcellations(method=method, n_parcels=5, mask=mask_img)
parcellator.fit(fmri_imgs)
```

## Next Steps


---

*Source: test_parcellations.py:188 | Complexity: Intermediate | Last updated: 2026-05-18*