# How To: Different Affines

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check mask and EIP files with different affines.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Check mask and EIP files with different affines.'

```python
'Check mask and EIP files with different affines.'
```

### Step 2: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(np.ones((2, 2, 2), dtype=np.int8), affine=np.diag((4, 4, 4, 1)))
```

### Step 3: Assign epi_img1 = Nifti1Image(...)

```python
epi_img1 = Nifti1Image(np.ones((4, 4, 4, 3)), affine=np.diag((2, 2, 2, 1)))
```

### Step 4: Assign epi_img2 = Nifti1Image(...)

```python
epi_img2 = Nifti1Image(np.ones((3, 3, 3, 3)), affine=np.diag((3, 3, 3, 1)))
```

### Step 5: Assign masker = MultiNiftiMasker(...)

```python
masker = MultiNiftiMasker(mask_img=mask_img, standardize=None)
```

### Step 6: Assign epis = masker.fit_transform(...)

```python
epis = masker.fit_transform([epi_img1, epi_img2])
```

### Step 7: Call masker.inverse_transform()

```python
masker.inverse_transform(this_epi)
```


## Complete Example

```python
# Workflow
'Check mask and EIP files with different affines.'
mask_img = Nifti1Image(np.ones((2, 2, 2), dtype=np.int8), affine=np.diag((4, 4, 4, 1)))
epi_img1 = Nifti1Image(np.ones((4, 4, 4, 3)), affine=np.diag((2, 2, 2, 1)))
epi_img2 = Nifti1Image(np.ones((3, 3, 3, 3)), affine=np.diag((3, 3, 3, 1)))
masker = MultiNiftiMasker(mask_img=mask_img, standardize=None)
epis = masker.fit_transform([epi_img1, epi_img2])
for this_epi in epis:
    masker.inverse_transform(this_epi)
```

## Next Steps


---

*Source: test_multi_nifti_masker.py:131 | Complexity: Intermediate | Last updated: 2026-05-18*