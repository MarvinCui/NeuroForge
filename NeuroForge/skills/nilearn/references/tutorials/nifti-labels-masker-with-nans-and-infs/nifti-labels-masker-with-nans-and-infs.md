# How To: Nifti Labels Masker With Nans And Infs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Deal with NaNs and infs in label image.

The masker should replace those NaNs and infs with zeros,
while raising a warning.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: affine_eye, n_regions, length, img_labels, img_fmri
```

## Step-by-Step Guide

### Step 1: 'Deal with NaNs and infs in label image.\n\n    The masker should replace those NaNs and infs with zeros,\n    while raising a warning.\n    '

```python
'Deal with NaNs and infs in label image.\n\n    The masker should replace those NaNs and infs with zeros,\n    while raising a warning.\n    '
```

**Verification:**
```python
assert len(unique) == n_regions + 3
```

### Step 2: Assign data = get_data.astype(...)

```python
data = get_data(img_labels).astype(np.float32)
```

**Verification:**
```python
assert 'nan' not in masker.lut_.name.to_list()
```

### Step 3: Assign unknown = value

```python
data[:, :, 7] = np.nan
```

**Verification:**
```python
assert 'inf' not in masker.lut_.name.to_list()
```

### Step 4: Assign unknown = value

```python
data[:, :, 4] = np.inf
```

**Verification:**
```python
assert 'unknown' not in masker.lut_.name.to_list()
```

### Step 5: Assign img_labels = Nifti1Image(...)

```python
img_labels = Nifti1Image(data, affine_eye)
```

**Verification:**
```python
assert np.all(np.isfinite(sig))
```

### Step 6: Assign unique = np.unique(...)

```python
unique = np.unique(data)
```

**Verification:**
```python
assert sig.shape == (length, n_regions)
```

### Step 7: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(img_labels, standardize=None)
```

**Verification:**
```python
assert 'nan' not in masker.lut_.name.to_list()
```

### Step 8: Assign sig = masker.fit_transform(...)

```python
sig = masker.fit_transform(img_fmri)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, n_regions, length, img_labels, img_fmri

# Workflow
'Deal with NaNs and infs in label image.\n\n    The masker should replace those NaNs and infs with zeros,\n    while raising a warning.\n    '
data = get_data(img_labels).astype(np.float32)
data[:, :, 7] = np.nan
data[:, :, 4] = np.inf
img_labels = Nifti1Image(data, affine_eye)
unique = np.unique(data)
assert len(unique) == n_regions + 3
masker = NiftiLabelsMasker(img_labels, standardize=None)
with pytest.warns(UserWarning, match='Non-finite values detected.'):
    sig = masker.fit_transform(img_fmri)
assert 'nan' not in masker.lut_.name.to_list()
assert 'inf' not in masker.lut_.name.to_list()
assert 'unknown' not in masker.lut_.name.to_list()
assert np.all(np.isfinite(sig))
assert sig.shape == (length, n_regions)
```

## Next Steps


---

*Source: test_nifti_labels_masker.py:181 | Complexity: Advanced | Last updated: 2026-05-18*