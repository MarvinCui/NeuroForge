# How To: Nan

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that the masker handles NaNs appropriately.

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

### Step 1: 'Check that the masker handles NaNs appropriately.'

```python
'Check that the masker handles NaNs appropriately.'
```

**Verification:**
```python
assert mask[1:-1, 1:-1, 1:-1].all()
```

### Step 2: Assign data = np.ones(...)

```python
data = np.ones((9, 9, 9))
```

**Verification:**
```python
assert not mask[0].any()
```

### Step 3: Assign unknown = value

```python
data[0] = np.nan
```

**Verification:**
```python
assert not mask[:, 0].any()
```

### Step 4: Assign unknown = value

```python
data[:, 0] = np.nan
```

**Verification:**
```python
assert not mask[:, :, 0].any()
```

### Step 5: Assign unknown = value

```python
data[:, :, 0] = np.nan
```

**Verification:**
```python
assert not mask[-1].any()
```

### Step 6: Assign unknown = value

```python
data[-1] = np.nan
```

**Verification:**
```python
assert not mask[:, -1].any()
```

### Step 7: Assign unknown = value

```python
data[:, -1] = np.nan
```

**Verification:**
```python
assert not mask[:, :, -1].any()
```

### Step 8: Assign unknown = value

```python
data[:, :, -1] = np.nan
```

### Step 9: Assign unknown = 10

```python
data[3:-3, 3:-3, 3:-3] = 10
```

### Step 10: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 11: Assign masker = NiftiMasker(...)

```python
masker = NiftiMasker(mask_args={'opening': 0})
```

### Step 12: Call masker.fit()

```python
masker.fit(img)
```

### Step 13: Assign mask = get_data(...)

```python
mask = get_data(masker.mask_img_)
```

**Verification:**
```python
assert mask[1:-1, 1:-1, 1:-1].all()
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Check that the masker handles NaNs appropriately.'
data = np.ones((9, 9, 9))
data[0] = np.nan
data[:, 0] = np.nan
data[:, :, 0] = np.nan
data[-1] = np.nan
data[:, -1] = np.nan
data[:, :, -1] = np.nan
data[3:-3, 3:-3, 3:-3] = 10
img = Nifti1Image(data, affine_eye)
masker = NiftiMasker(mask_args={'opening': 0})
masker.fit(img)
mask = get_data(masker.mask_img_)
assert mask[1:-1, 1:-1, 1:-1].all()
assert not mask[0].any()
assert not mask[:, 0].any()
assert not mask[:, :, 0].any()
assert not mask[-1].any()
assert not mask[:, -1].any()
assert not mask[:, :, -1].any()
```

## Next Steps


---

*Source: test_nifti_masker.py:155 | Complexity: Advanced | Last updated: 2026-05-18*