# How To: High Variance Confounds Surface

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check high_variance_confounds returns proper shape from surface.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `re`
- `warnings`
- `collections.abc`
- `pathlib`
- `joblib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `nibabel.freesurfer`
- `numpy.testing`
- `nilearn`
- `nilearn`
- `nilearn._utils`
- `nilearn._utils.data_gen`
- `nilearn._utils.niimg`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image.image`
- `nilearn.image.resampling`
- `nilearn.image.tests._testing`
- `nilearn.surface.surface`
- `nilearn.surface.surface`
- `nilearn.surface.utils`

**Setup Required:**
```python
# Fixtures: surf_mask_1d, surface_glm_data
```

## Step-by-Step Guide

### Step 1: 'Check high_variance_confounds returns proper shape from surface.'

```python
'Check high_variance_confounds returns proper shape from surface.'
```

**Verification:**
```python
assert confounds1.shape == (length, n_confounds)
```

### Step 2: Assign length = 17

```python
length = 17
```

**Verification:**
```python
assert confounds2.shape == (length, n_confounds)
```

### Step 3: Assign n_confounds = 10

```python
n_confounds = 10
```

### Step 4: Assign unknown = surface_glm_data(...)

```python
img, _ = surface_glm_data(length)
```

### Step 5: Assign confounds1 = high_variance_confounds(...)

```python
confounds1 = high_variance_confounds(img, mask_img=surf_mask_1d, percentile=10.0, n_confounds=n_confounds)
```

**Verification:**
```python
assert confounds1.shape == (length, n_confounds)
```

### Step 6: Assign confounds2 = high_variance_confounds(...)

```python
confounds2 = high_variance_confounds(img, percentile=10.0, n_confounds=n_confounds)
```

**Verification:**
```python
assert confounds2.shape == (length, n_confounds)
```


## Complete Example

```python
# Setup
# Fixtures: surf_mask_1d, surface_glm_data

# Workflow
'Check high_variance_confounds returns proper shape from surface.'
length = 17
n_confounds = 10
img, _ = surface_glm_data(length)
confounds1 = high_variance_confounds(img, mask_img=surf_mask_1d, percentile=10.0, n_confounds=n_confounds)
assert confounds1.shape == (length, n_confounds)
confounds2 = high_variance_confounds(img, percentile=10.0, n_confounds=n_confounds)
assert confounds2.shape == (length, n_confounds)
```

## Next Steps


---

*Source: test_image.py:238 | Complexity: Intermediate | Last updated: 2026-05-18*