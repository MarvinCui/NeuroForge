# How To: Nifti Maps Masker With Nans And Infs In Data

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Apply a NiftiMapsMasker to 4D data containing NaNs and infs.

The masker should replace those NaNs and infs with zeros,
while raising a warning.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.testing`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: length, n_regions, affine_eye
```

## Step-by-Step Guide

### Step 1: 'Apply a NiftiMapsMasker to 4D data containing NaNs and infs.\n\n    The masker should replace those NaNs and infs with zeros,\n    while raising a warning.\n    '

```python
'Apply a NiftiMapsMasker to 4D data containing NaNs and infs.\n\n    The masker should replace those NaNs and infs with zeros,\n    while raising a warning.\n    '
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 2: Assign unknown = generate_random_img(...)

```python
fmri_img, mask_img = generate_random_img((13, 11, 12, length), affine=affine_eye)
```

**Verification:**
```python
assert np.all(np.isfinite(signals))
```

### Step 3: Assign unknown = generate_maps(...)

```python
maps_img, _ = generate_maps((13, 11, 12), n_regions, affine=affine_eye)
```

### Step 4: Assign fmri_data = get_data(...)

```python
fmri_data = get_data(fmri_img)
```

### Step 5: Assign unknown = value

```python
fmri_data[:, 9, 9, :] = np.nan
```

### Step 6: Assign unknown = value

```python
fmri_data[:, 5, 5, :] = np.inf
```

### Step 7: Assign fmri_img = Nifti1Image(...)

```python
fmri_img = Nifti1Image(fmri_data, affine_eye)
```

### Step 8: Assign masker = NiftiMapsMasker(...)

```python
masker = NiftiMapsMasker(maps_img, mask_img=mask_img, standardize=None)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 9: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri_img)
```


## Complete Example

```python
# Setup
# Fixtures: length, n_regions, affine_eye

# Workflow
'Apply a NiftiMapsMasker to 4D data containing NaNs and infs.\n\n    The masker should replace those NaNs and infs with zeros,\n    while raising a warning.\n    '
fmri_img, mask_img = generate_random_img((13, 11, 12, length), affine=affine_eye)
maps_img, _ = generate_maps((13, 11, 12), n_regions, affine=affine_eye)
fmri_data = get_data(fmri_img)
fmri_data[:, 9, 9, :] = np.nan
fmri_data[:, 5, 5, :] = np.inf
fmri_img = Nifti1Image(fmri_data, affine_eye)
masker = NiftiMapsMasker(maps_img, mask_img=mask_img, standardize=None)
with pytest.warns(UserWarning, match='Non-finite values detected.'):
    signals = masker.fit_transform(fmri_img)
assert signals.shape == (length, n_regions)
assert np.all(np.isfinite(signals))
```

## Next Steps


---

*Source: test_nifti_maps_masker.py:240 | Complexity: Advanced | Last updated: 2026-05-18*