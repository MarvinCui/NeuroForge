# How To: Check Embedded Masker Attribute Forwarding

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check attribute forwarding.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `joblib`
- `nibabel`
- `sklearn.base`
- `nilearn._base`
- `nilearn._utils.versions`
- `nilearn.maskers`
- `nilearn.maskers.masker_validation`
- `nilearn._utils.tags`
- `nilearn._utils.tags`
- `nilearn._utils.tags`
- `nilearn._utils.tags`


## Step-by-Step Guide

### Step 1: 'Check attribute forwarding.'

```python
'Check attribute forwarding.'
```

**Verification:**
```python
assert masker.mask_img is mask.mask_img_
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((9, 9, 9))
```

### Step 3: Assign unknown = 10

```python
data[2:-2, 2:-2, 2:-2] = 10
```

### Step 4: Assign imgs = Nifti1Image(...)

```python
imgs = Nifti1Image(data, np.eye(4))
```

### Step 5: Assign mask = MultiNiftiMasker(...)

```python
mask = MultiNiftiMasker()
```

### Step 6: Call mask.fit()

```python
mask.fit([[imgs]])
```

### Step 7: Assign owner = OwningClass(...)

```python
owner = OwningClass(mask=mask)
```

### Step 8: Assign masker = check_embedded_masker(...)

```python
masker = check_embedded_masker(owner, masker_type='nii')
```

**Verification:**
```python
assert masker.mask_img is mask.mask_img_
```


## Complete Example

```python
# Workflow
'Check attribute forwarding.'
data = np.zeros((9, 9, 9))
data[2:-2, 2:-2, 2:-2] = 10
imgs = Nifti1Image(data, np.eye(4))
mask = MultiNiftiMasker()
mask.fit([[imgs]])
owner = OwningClass(mask=mask)
masker = check_embedded_masker(owner, masker_type='nii')
assert masker.mask_img is mask.mask_img_
```

## Next Steps


---

*Source: test_masker_validation.py:202 | Complexity: Advanced | Last updated: 2026-05-18*