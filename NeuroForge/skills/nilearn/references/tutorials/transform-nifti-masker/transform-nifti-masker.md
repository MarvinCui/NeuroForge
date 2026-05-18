# How To: Transform Nifti Masker

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Smoke test that 'mask' can be (multi)NiftiMasker.

Regression test for https://github.com/nilearn/nilearn/issues/5926

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
# Fixtures: masker, image_2, affine_eye
```

## Step-by-Step Guide

### Step 1: "Smoke test that 'mask' can be (multi)NiftiMasker.\n\n    Regression test for https://github.com/nilearn/nilearn/issues/5926\n    "

```python
"Smoke test that 'mask' can be (multi)NiftiMasker.\n\n    Regression test for https://github.com/nilearn/nilearn/issues/5926\n    "
```

### Step 2: Assign fmri_imgs = value

```python
fmri_imgs = [image_2] * 3
```

### Step 3: Assign mask_img = np.ones(...)

```python
mask_img = np.ones((10, 11, 12))
```

### Step 4: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask_img, affine_eye)
```

### Step 5: Assign mask = masker(...)

```python
mask = masker(mask_img=mask_img)
```

### Step 6: Assign parcellator = Parcellations(...)

```python
parcellator = Parcellations(method='kmeans', mask=mask)
```

### Step 7: Call parcellator.fit()

```python
parcellator.fit(fmri_imgs)
```

### Step 8: Call parcellator.transform()

```python
parcellator.transform(fmri_imgs)
```


## Complete Example

```python
# Setup
# Fixtures: masker, image_2, affine_eye

# Workflow
"Smoke test that 'mask' can be (multi)NiftiMasker.\n\n    Regression test for https://github.com/nilearn/nilearn/issues/5926\n    "
fmri_imgs = [image_2] * 3
mask_img = np.ones((10, 11, 12))
mask_img = Nifti1Image(mask_img, affine_eye)
mask = masker(mask_img=mask_img)
parcellator = Parcellations(method='kmeans', mask=mask)
parcellator.fit(fmri_imgs)
parcellator.transform(fmri_imgs)
```

## Next Steps


---

*Source: test_parcellations.py:255 | Complexity: Advanced | Last updated: 2026-05-18*