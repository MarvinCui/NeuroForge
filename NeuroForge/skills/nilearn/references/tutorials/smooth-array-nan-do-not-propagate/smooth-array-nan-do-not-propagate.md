# How To: Smooth Array Nan Do Not Propagate

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test smooth array nan do not propagate

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign data = _new_data_for_smooth_array(...)

```python
data = _new_data_for_smooth_array()
```

**Verification:**
```python
assert np.all(np.isfinite(filtered))
```

### Step 2: Assign unknown = value

```python
data[10, 10, 10] = np.nan
```

### Step 3: Assign fwhm = 9

```python
fwhm = 9
```

### Step 4: Assign affine = value

```python
affine = AFFINE_TO_TEST[2]
```

### Step 5: Assign filtered = smooth_array(...)

```python
filtered = smooth_array(data, affine, fwhm=fwhm, ensure_finite=True, copy=True)
```

**Verification:**
```python
assert np.all(np.isfinite(filtered))
```


## Complete Example

```python
# Workflow
data = _new_data_for_smooth_array()
data[10, 10, 10] = np.nan
fwhm = 9
affine = AFFINE_TO_TEST[2]
filtered = smooth_array(data, affine, fwhm=fwhm, ensure_finite=True, copy=True)
assert np.all(np.isfinite(filtered))
```

## Next Steps


---

*Source: test_image.py:315 | Complexity: Intermediate | Last updated: 2026-05-18*