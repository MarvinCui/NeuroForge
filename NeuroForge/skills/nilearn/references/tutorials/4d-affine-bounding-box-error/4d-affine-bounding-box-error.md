# How To: 4D Affine Bounding Box Error

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 4d affine bounding box error

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

### Step 1: Assign bigger_data = np.zeros(...)

```python
bigger_data = np.zeros([10, 10, 10])
```

**Verification:**
```python
assert_almost_equal(l2_norm(small_data), l2_norm(get_data(small_to_big_with_shape)))
```

### Step 2: Assign bigger_img = Nifti1Image(...)

```python
bigger_img = Nifti1Image(bigger_data, affine_eye)
```

**Verification:**
```python
assert_almost_equal(l2_norm(small_data), l2_norm(get_data(small_to_big_without_shape_3D_affine)))
```

### Step 3: Assign small_data = np.ones(...)

```python
small_data = np.ones([4, 4, 4])
```

**Verification:**
```python
assert_almost_equal(l2_norm(small_data), l2_norm(get_data(small_to_big_without_shape)))
```

### Step 4: Assign small_data_4D_affine = affine_eye

```python
small_data_4D_affine = affine_eye
```

**Verification:**
```python
assert_array_equal(small_to_big_without_shape.shape, small_data_4D_affine[:3, -1] + np.array(small_img.shape))
```

### Step 5: Assign unknown = np.array(...)

```python
small_data_4D_affine[:3, -1] = np.array([5, 4, 5])
```

### Step 6: Assign small_img = Nifti1Image(...)

```python
small_img = Nifti1Image(small_data, small_data_4D_affine)
```

### Step 7: Assign small_to_big_with_shape = resample_img(...)

```python
small_to_big_with_shape = resample_img(small_img, target_affine=bigger_img.affine, target_shape=bigger_img.shape, force_resample=force_resample)
```

### Step 8: Assign small_to_big_without_shape_3D_affine = resample_img(...)

```python
small_to_big_without_shape_3D_affine = resample_img(small_img, target_affine=bigger_img.affine[:3, :3], force_resample=force_resample)
```

### Step 9: Assign small_to_big_without_shape = resample_img(...)

```python
small_to_big_without_shape = resample_img(small_img, target_affine=bigger_img.affine, force_resample=force_resample)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(l2_norm(small_data), l2_norm(get_data(small_to_big_with_shape)))
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(l2_norm(small_data), l2_norm(get_data(small_to_big_without_shape_3D_affine)))
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(l2_norm(small_data), l2_norm(get_data(small_to_big_without_shape)))
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(small_to_big_without_shape.shape, small_data_4D_affine[:3, -1] + np.array(small_img.shape))
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, force_resample

# Workflow
bigger_data = np.zeros([10, 10, 10])
bigger_img = Nifti1Image(bigger_data, affine_eye)
small_data = np.ones([4, 4, 4])
small_data_4D_affine = affine_eye
small_data_4D_affine[:3, -1] = np.array([5, 4, 5])
small_img = Nifti1Image(small_data, small_data_4D_affine)

def l2_norm(arr):
    return (arr ** 2).sum()
small_to_big_with_shape = resample_img(small_img, target_affine=bigger_img.affine, target_shape=bigger_img.shape, force_resample=force_resample)
small_to_big_without_shape_3D_affine = resample_img(small_img, target_affine=bigger_img.affine[:3, :3], force_resample=force_resample)
small_to_big_without_shape = resample_img(small_img, target_affine=bigger_img.affine, force_resample=force_resample)
assert_almost_equal(l2_norm(small_data), l2_norm(get_data(small_to_big_with_shape)))
assert_almost_equal(l2_norm(small_data), l2_norm(get_data(small_to_big_without_shape_3D_affine)))
assert_almost_equal(l2_norm(small_data), l2_norm(get_data(small_to_big_without_shape)))
assert_array_equal(small_to_big_without_shape.shape, small_data_4D_affine[:3, -1] + np.array(small_img.shape))
```

## Next Steps


---

*Source: test_resampling.py:487 | Complexity: Advanced | Last updated: 2026-05-18*