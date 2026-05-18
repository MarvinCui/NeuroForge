# How To: Inverse Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Applying the sphere_extraction example from above backwards.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng, affine_eye
```

## Step-by-Step Guide

### Step 1: 'Applying the sphere_extraction example from above backwards.'

```python
'Applying the sphere_extraction example from above backwards.'
```

**Verification:**
```python
assert_array_equal(np.mean(get_data(inverse_map), axis=-1) != 0, array_mask)
```

### Step 2: Assign data = rng.random(...)

```python
data = rng.random((3, 3, 3, 5))
```

**Verification:**
```python
assert_array_equal(get_data(inverse_map)[array_mask].mean(0), s[:, 0])
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

**Verification:**
```python
assert_array_equal(inverse_map.shape[:3], mask_img.shape)
```

### Step 4: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker([(1, 1, 1)], radius=1, standardize=None)
```

### Step 5: Call masker.fit()

```python
masker.fit()
```

### Step 6: Assign signal = masker.transform(...)

```python
signal = masker.transform(img)
```

### Step 7: Assign mask_img = np.zeros(...)

```python
mask_img = np.zeros((3, 3, 3))
```

### Step 8: Assign unknown = 1

```python
mask_img[1, :, :] = 1
```

### Step 9: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask_img, affine_eye)
```

### Step 10: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker([(1, 1, 1)], radius=1, mask_img=mask_img, standardize=None)
```

### Step 11: Call masker.fit()

```python
masker.fit()
```

### Step 12: Assign s = masker.transform(...)

```python
s = masker.transform(img)
```

### Step 13: Assign mask = np.zeros(...)

```python
mask = np.zeros((3, 3, 3), dtype=bool)
```

### Step 14: Assign unknown = True

```python
mask[:, 1, 1] = True
```

### Step 15: Assign unknown = True

```python
mask[1, :, 1] = True
```

### Step 16: Assign unknown = True

```python
mask[1, 1, :] = True
```

### Step 17: Assign array_mask = np.logical_and(...)

```python
array_mask = np.logical_and(mask, get_data(mask_img))
```

### Step 18: Assign inverse_map = masker.inverse_transform(...)

```python
inverse_map = masker.inverse_transform(s)
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(np.mean(get_data(inverse_map), axis=-1) != 0, array_mask)
```

### Step 20: Call assert_array_equal()

```python
assert_array_equal(get_data(inverse_map)[array_mask].mean(0), s[:, 0])
```

### Step 21: Call assert_array_equal()

```python
assert_array_equal(inverse_map.shape[:3], mask_img.shape)
```

### Step 22: Call masker.inverse_transform()

```python
masker.inverse_transform(signal)
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye

# Workflow
'Applying the sphere_extraction example from above backwards.'
data = rng.random((3, 3, 3, 5))
img = Nifti1Image(data, affine_eye)
masker = NiftiSpheresMasker([(1, 1, 1)], radius=1, standardize=None)
masker.fit()
signal = masker.transform(img)
with pytest.raises(ValueError, match='Please provide mask_img'):
    masker.inverse_transform(signal)
mask_img = np.zeros((3, 3, 3))
mask_img[1, :, :] = 1
mask_img = Nifti1Image(mask_img, affine_eye)
masker = NiftiSpheresMasker([(1, 1, 1)], radius=1, mask_img=mask_img, standardize=None)
masker.fit()
s = masker.transform(img)
mask = np.zeros((3, 3, 3), dtype=bool)
mask[:, 1, 1] = True
mask[1, :, 1] = True
mask[1, 1, :] = True
array_mask = np.logical_and(mask, get_data(mask_img))
inverse_map = masker.inverse_transform(s)
assert_array_equal(np.mean(get_data(inverse_map), axis=-1) != 0, array_mask)
assert_array_equal(get_data(inverse_map)[array_mask].mean(0), s[:, 0])
assert_array_equal(inverse_map.shape[:3], mask_img.shape)
```

## Next Steps


---

*Source: test_nifti_spheres_masker.py:281 | Complexity: Advanced | Last updated: 2026-05-18*