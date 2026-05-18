# How To: Multi Nifti Maps Masker Errors

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check errors raised by MultiNiftiMapsMasker.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.testing`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: affine_eye, length, shape_3d_default, img_maps
```

## Step-by-Step Guide

### Step 1: 'Check errors raised by MultiNiftiMapsMasker.'

```python
'Check errors raised by MultiNiftiMapsMasker.'
```

### Step 2: Assign unknown = generate_fake_fmri(...)

```python
fmri11_img, mask11_img = generate_fake_fmri(shape_3d_default, affine=affine_eye, length=length)
```

### Step 3: Assign masker = MultiNiftiMapsMasker(...)

```python
masker = MultiNiftiMapsMasker(img_maps, mask_img=mask11_img, resampling_target=None, standardize=None)
```

### Step 4: Assign signals_input = value

```python
signals_input = [fmri11_img, fmri11_img]
```

### Step 5: Assign masker = NiftiMapsMasker(...)

```python
masker = NiftiMapsMasker(img_maps, resampling_target=None, standardize=None)
```

### Step 6: Call masker.fit_transform()

```python
masker.fit_transform(signals_input)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, length, shape_3d_default, img_maps

# Workflow
'Check errors raised by MultiNiftiMapsMasker.'
fmri11_img, mask11_img = generate_fake_fmri(shape_3d_default, affine=affine_eye, length=length)
masker = MultiNiftiMapsMasker(img_maps, mask_img=mask11_img, resampling_target=None, standardize=None)
signals_input = [fmri11_img, fmri11_img]
masker = NiftiMapsMasker(img_maps, resampling_target=None, standardize=None)
with pytest.raises(DimensionError, match='incompatible dimensionality'):
    masker.fit_transform(signals_input)
```

## Next Steps


---

*Source: test_multi_nifti_maps_masker.py:155 | Complexity: Intermediate | Last updated: 2026-05-18*