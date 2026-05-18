# How To: 3X3 Affine Bbox

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that the bounding-box is properly computed when     transforming with a negative affine component.

This is specifically to test for a change in behavior between
scipy < 0.18 and scipy >= 0.18, which is an interaction between
offset and a diagonal affine

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `math`
- `os`
- `sys`
- `pathlib`
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.freesurfer`
- `numpy.testing`
- `nilearn._utils`
- `nilearn._utils.niimg`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.image.image`
- `nilearn.image.resampling`
- `nilearn.image.tests._testing`

**Setup Required:**
```python
# Fixtures: affine_eye, force_resample
```

## Step-by-Step Guide

### Step 1: 'Test that the bounding-box is properly computed when     transforming with a negative affine component.\n\n    This is specifically to test for a change in behavior between\n    scipy < 0.18 and scipy >= 0.18, which is an interaction between\n    offset and a diagonal affine\n    '

```python
'Test that the bounding-box is properly computed when     transforming with a negative affine component.\n\n    This is specifically to test for a change in behavior between\n    scipy < 0.18 and scipy >= 0.18, which is an interaction between\n    offset and a diagonal affine\n    '
```

**Verification:**
```python
assert_allclose(get_data(img_3d_affine).max(), image.max())
```

### Step 2: Assign image = np.ones(...)

```python
image = np.ones((20, 30))
```

### Step 3: Assign source_affine = affine_eye

```python
source_affine = affine_eye
```

### Step 4: Assign unknown = np.array(...)

```python
source_affine[:2, 3] = np.array([96, 64])
```

### Step 5: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(image[:, :, np.newaxis], affine=source_affine)
```

### Step 6: Assign target_affine_3x3 = value

```python
target_affine_3x3 = np.eye(3) * 2
```

### Step 7: Assign img_3d_affine = resample_img(...)

```python
img_3d_affine = resample_img(img, target_affine=target_affine_3x3, force_resample=force_resample)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(get_data(img_3d_affine).max(), image.max())
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, force_resample

# Workflow
'Test that the bounding-box is properly computed when     transforming with a negative affine component.\n\n    This is specifically to test for a change in behavior between\n    scipy < 0.18 and scipy >= 0.18, which is an interaction between\n    offset and a diagonal affine\n    '
image = np.ones((20, 30))
source_affine = affine_eye
source_affine[:2, 3] = np.array([96, 64])
img = Nifti1Image(image[:, :, np.newaxis], affine=source_affine)
target_affine_3x3 = np.eye(3) * 2
target_affine_3x3[1] *= -1
img_3d_affine = resample_img(img, target_affine=target_affine_3x3, force_resample=force_resample)
assert_allclose(get_data(img_3d_affine).max(), image.max())
```

## Next Steps


---

*Source: test_resampling.py:564 | Complexity: Advanced | Last updated: 2026-05-18*