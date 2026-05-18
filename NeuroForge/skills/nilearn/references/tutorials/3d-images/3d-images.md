# How To: 3D Images

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that the MultiNiftiMasker works with 3D images.

Note that fit() requires all images in list to have the same affine.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test that the MultiNiftiMasker works with 3D images.\n\n    Note that fit() requires all images in list to have the same affine.\n    '

```python
'Test that the MultiNiftiMasker works with 3D images.\n\n    Note that fit() requires all images in list to have the same affine.\n    '
```

### Step 2: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(np.ones((2, 2, 2), dtype=np.int8), affine=np.diag((2, 2, 2, 1)))
```

### Step 3: Assign epi_img1 = Nifti1Image(...)

```python
epi_img1 = Nifti1Image(rng.random((2, 2, 2)), affine=np.diag((4, 4, 4, 1)))
```

### Step 4: Assign epi_img2 = Nifti1Image(...)

```python
epi_img2 = Nifti1Image(rng.random((2, 2, 2)), affine=np.diag((4, 4, 4, 1)))
```

### Step 5: Assign masker = MultiNiftiMasker(...)

```python
masker = MultiNiftiMasker(mask_img=mask_img, standardize=None)
```

### Step 6: Call masker.fit_transform()

```python
masker.fit_transform([epi_img1, epi_img2])
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test that the MultiNiftiMasker works with 3D images.\n\n    Note that fit() requires all images in list to have the same affine.\n    '
mask_img = Nifti1Image(np.ones((2, 2, 2), dtype=np.int8), affine=np.diag((2, 2, 2, 1)))
epi_img1 = Nifti1Image(rng.random((2, 2, 2)), affine=np.diag((4, 4, 4, 1)))
epi_img2 = Nifti1Image(rng.random((2, 2, 2)), affine=np.diag((4, 4, 4, 1)))
masker = MultiNiftiMasker(mask_img=mask_img, standardize=None)
masker.fit_transform([epi_img1, epi_img2])
```

## Next Steps


---

*Source: test_multi_nifti_masker.py:146 | Complexity: Intermediate | Last updated: 2026-05-18*