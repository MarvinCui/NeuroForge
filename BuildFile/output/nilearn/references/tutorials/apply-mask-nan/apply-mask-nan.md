# How To: Apply Mask Nan

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that NaNs in the data do not propagate.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.preprocessing`
- `nilearn._utils`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.masking`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: 'Check that NaNs in the data do not propagate.'

```python
'Check that NaNs in the data do not propagate.'
```

**Verification:**
```python
assert np.all(np.isfinite(series))
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((40, 40, 40, 2))
```

### Step 3: Assign unknown = 1

```python
data[20, 20, 20] = 1
```

### Step 4: Assign unknown = value

```python
data[10, 10, 10] = np.nan
```

### Step 5: Assign data_img = Nifti1Image(...)

```python
data_img = Nifti1Image(data, affine_eye)
```

### Step 6: Assign mask = np.ones(...)

```python
mask = np.ones((40, 40, 40))
```

### Step 7: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask, affine_eye)
```

### Step 8: Assign series = apply_mask(...)

```python
series = apply_mask(data_img, mask_img, smoothing_fwhm=9)
```

**Verification:**
```python
assert np.all(np.isfinite(series))
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Check that NaNs in the data do not propagate.'
data = np.zeros((40, 40, 40, 2))
data[20, 20, 20] = 1
data[10, 10, 10] = np.nan
data_img = Nifti1Image(data, affine_eye)
mask = np.ones((40, 40, 40))
mask_img = Nifti1Image(mask, affine_eye)
series = apply_mask(data_img, mask_img, smoothing_fwhm=9)
assert np.all(np.isfinite(series))
```

## Next Steps


---

*Source: test_masking.py:407 | Complexity: Advanced | Last updated: 2026-05-18*