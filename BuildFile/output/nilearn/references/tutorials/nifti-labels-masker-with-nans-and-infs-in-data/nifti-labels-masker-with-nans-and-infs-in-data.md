# How To: Nifti Labels Masker With Nans And Infs In Data

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Apply a NiftiLabelsMasker to 4D data containing NaNs and infs.

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
# Fixtures: affine_eye, img_fmri, n_regions, length, img_labels
```

## Step-by-Step Guide

### Step 1: 'Apply a NiftiLabelsMasker to 4D data containing NaNs and infs.\n\n    The masker should replace those NaNs and infs with zeros,\n    while raising a warning.\n    '

```python
'Apply a NiftiLabelsMasker to 4D data containing NaNs and infs.\n\n    The masker should replace those NaNs and infs with zeros,\n    while raising a warning.\n    '
```

**Verification:**
```python
assert np.all(np.isfinite(sig))
```

### Step 2: Assign fmri_data = get_data.astype(...)

```python
fmri_data = get_data(img_fmri).astype(np.float32)
```

**Verification:**
```python
assert sig.shape == (length, n_regions)
```

### Step 3: Assign unknown = value

```python
fmri_data[:, :, 7, :] = np.nan
```

### Step 4: Assign unknown = value

```python
fmri_data[:, :, 4, 0] = np.inf
```

### Step 5: Assign fmri_img = Nifti1Image(...)

```python
fmri_img = Nifti1Image(fmri_data, affine_eye)
```

### Step 6: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(img_labels, standardize=None)
```

**Verification:**
```python
assert np.all(np.isfinite(sig))
```

### Step 7: Assign sig = masker.fit_transform(...)

```python
sig = masker.fit_transform(fmri_img)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, img_fmri, n_regions, length, img_labels

# Workflow
'Apply a NiftiLabelsMasker to 4D data containing NaNs and infs.\n\n    The masker should replace those NaNs and infs with zeros,\n    while raising a warning.\n    '
fmri_data = get_data(img_fmri).astype(np.float32)
fmri_data[:, :, 7, :] = np.nan
fmri_data[:, :, 4, 0] = np.inf
fmri_img = Nifti1Image(fmri_data, affine_eye)
masker = NiftiLabelsMasker(img_labels, standardize=None)
with pytest.warns(UserWarning, match='Non-finite values detected.'):
    sig = masker.fit_transform(fmri_img)
assert np.all(np.isfinite(sig))
assert sig.shape == (length, n_regions)
```

## Next Steps


---

*Source: test_nifti_labels_masker.py:213 | Complexity: Intermediate | Last updated: 2026-05-18*