# How To: Smooth Img Surface 2D

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test smoothing surface images 2d.

Ensure we get equivalent result that smoothing a list of image.

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
# Fixtures: surf_img_2d
```

## Step-by-Step Guide

### Step 1: 'Test smoothing surface images 2d.\n\n    Ensure we get equivalent result that smoothing a list of image.\n    '

```python
'Test smoothing surface images 2d.\n\n    Ensure we get equivalent result that smoothing a list of image.\n    '
```

**Verification:**
```python
assert isinstance(smoothed_img, SurfaceImage)
```

### Step 2: Assign img = surf_img_2d(...)

```python
img = surf_img_2d(3)
```

**Verification:**
```python
assert_array_equal(get_surface_data(x), get_surface_data(index_img(smoothed_img, i)))
```

### Step 3: Assign smoothed_img = smooth_img(...)

```python
smoothed_img = smooth_img(img, fwhm=5)
```

**Verification:**
```python
assert isinstance(smoothed_img, SurfaceImage)
```

### Step 4: Assign img_as_list = list(...)

```python
img_as_list = list(iter_img(img))
```

### Step 5: Assign smoothed_img_as_list = smooth_img(...)

```python
smoothed_img_as_list = smooth_img(img_as_list, fwhm=5)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(get_surface_data(x), get_surface_data(index_img(smoothed_img, i)))
```


## Complete Example

```python
# Setup
# Fixtures: surf_img_2d

# Workflow
'Test smoothing surface images 2d.\n\n    Ensure we get equivalent result that smoothing a list of image.\n    '
img = surf_img_2d(3)
smoothed_img = smooth_img(img, fwhm=5)
assert isinstance(smoothed_img, SurfaceImage)
img_as_list = list(iter_img(img))
smoothed_img_as_list = smooth_img(img_as_list, fwhm=5)
for i, x in enumerate(smoothed_img_as_list):
    assert_array_equal(get_surface_data(x), get_surface_data(index_img(smoothed_img, i)))
```

## Next Steps


---

*Source: test_image.py:463 | Complexity: Intermediate | Last updated: 2026-05-18*