# How To: Smooth Img Surface

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test smoothing surface images.

Test output equal when fwhm=None and fwhm=0.
Test smoothing changes input.
Test that min and max are less extreme after smoothing.

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
# Fixtures: surf_img_1d
```

## Step-by-Step Guide

### Step 1: 'Test smoothing surface images.\n\n    Test output equal when fwhm=None and fwhm=0.\n    Test smoothing changes input.\n    Test that min and max are less extreme after smoothing.\n    '

```python
'Test smoothing surface images.\n\n    Test output equal when fwhm=None and fwhm=0.\n    Test smoothing changes input.\n    Test that min and max are less extreme after smoothing.\n    '
```

**Verification:**
```python
assert_surface_image_equal(surf_img_1d, out_fwhm_zero)
```

### Step 2: Assign out_fwhm_none = smooth_img(...)

```python
out_fwhm_none = smooth_img(surf_img_1d, fwhm=None)
```

**Verification:**
```python
assert_surface_image_equal(out_fwhm_none, out_fwhm_zero)
```

### Step 3: Assign out_fwhm_zero = smooth_img(...)

```python
out_fwhm_zero = smooth_img(surf_img_1d, fwhm=0)
```

**Verification:**
```python
assert_surface_image_equal(smoothed_img, surf_img_1d)
```

### Step 4: Call assert_surface_image_equal()

```python
assert_surface_image_equal(surf_img_1d, out_fwhm_zero)
```

**Verification:**
```python
assert data.max() > smoothed_data.max()
```

### Step 5: Call assert_surface_image_equal()

```python
assert_surface_image_equal(out_fwhm_none, out_fwhm_zero)
```

**Verification:**
```python
assert data.min() < smoothed_data.min()
```

### Step 6: Assign smoothed_img = smooth_img(...)

```python
smoothed_img = smooth_img(surf_img_1d, fwhm=5)
```

**Verification:**
```python
assert data.var() > smoothed_data.var()
```

### Step 7: Assign data = get_surface_data(...)

```python
data = get_surface_data(surf_img_1d)
```

### Step 8: Assign smoothed_data = get_surface_data(...)

```python
smoothed_data = get_surface_data(smoothed_img)
```

**Verification:**
```python
assert data.max() > smoothed_data.max()
```

### Step 9: Call assert_surface_image_equal()

```python
assert_surface_image_equal(smoothed_img, surf_img_1d)
```


## Complete Example

```python
# Setup
# Fixtures: surf_img_1d

# Workflow
'Test smoothing surface images.\n\n    Test output equal when fwhm=None and fwhm=0.\n    Test smoothing changes input.\n    Test that min and max are less extreme after smoothing.\n    '
out_fwhm_none = smooth_img(surf_img_1d, fwhm=None)
out_fwhm_zero = smooth_img(surf_img_1d, fwhm=0)
assert_surface_image_equal(surf_img_1d, out_fwhm_zero)
assert_surface_image_equal(out_fwhm_none, out_fwhm_zero)
smoothed_img = smooth_img(surf_img_1d, fwhm=5)
with pytest.raises(ValueError, match="Part 'left' of PolyData instances are not equal"):
    assert_surface_image_equal(smoothed_img, surf_img_1d)
data = get_surface_data(surf_img_1d)
smoothed_data = get_surface_data(smoothed_img)
assert data.max() > smoothed_data.max()
assert data.min() < smoothed_data.min()
assert data.var() > smoothed_data.var()
```

## Next Steps


---

*Source: test_image.py:424 | Complexity: Advanced | Last updated: 2026-05-18*