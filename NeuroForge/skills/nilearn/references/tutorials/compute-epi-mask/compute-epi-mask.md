# How To: Compute Epi Mask

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test compute_epi_mask.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.preprocessing`
- `nilearn._utils`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.masking`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: 'Test compute_epi_mask.'

```python
'Test compute_epi_mask.'
```

**Verification:**
```python
assert_array_equal(get_data(mask1), get_data(mask2))
```

### Step 2: Assign mean_image = np.ones(...)

```python
mean_image = np.ones((9, 9, 3))
```

**Verification:**
```python
assert_array_equal(get_data(mask1), get_data(mask3)[3:12, 3:12])
```

### Step 3: Assign unknown = 10

```python
mean_image[3:-2, 3:-2, :] = 10
```

**Verification:**
```python
assert not np.allclose(get_data(mask1), get_data(mask3)[3:12, 3:12])
```

### Step 4: Assign unknown = 11

```python
mean_image[5, 5, :] = 11
```

### Step 5: Assign mean_image = Nifti1Image(...)

```python
mean_image = Nifti1Image(mean_image, affine_eye)
```

### Step 6: Assign mask1 = compute_epi_mask(...)

```python
mask1 = compute_epi_mask(mean_image, opening=False, verbose=1)
```

### Step 7: Assign mask2 = compute_epi_mask(...)

```python
mask2 = compute_epi_mask(mean_image, exclude_zeros=True, opening=False)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(get_data(mask1), get_data(mask2))
```

### Step 9: Assign mean_image2 = np.zeros(...)

```python
mean_image2 = np.zeros((30, 30, 3))
```

### Step 10: Assign unknown = get_data(...)

```python
mean_image2[3:12, 3:12, :] = get_data(mean_image)
```

### Step 11: Assign mean_image2 = Nifti1Image(...)

```python
mean_image2 = Nifti1Image(mean_image2, affine_eye)
```

### Step 12: Assign mask3 = compute_epi_mask(...)

```python
mask3 = compute_epi_mask(mean_image2, exclude_zeros=True, opening=False)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(get_data(mask1), get_data(mask3)[3:12, 3:12])
```

### Step 14: Assign mask3 = compute_epi_mask(...)

```python
mask3 = compute_epi_mask(mean_image2, opening=False)
```

**Verification:**
```python
assert not np.allclose(get_data(mask1), get_data(mask3)[3:12, 3:12])
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Test compute_epi_mask.'
mean_image = np.ones((9, 9, 3))
mean_image[3:-2, 3:-2, :] = 10
mean_image[5, 5, :] = 11
mean_image = Nifti1Image(mean_image, affine_eye)
mask1 = compute_epi_mask(mean_image, opening=False, verbose=1)
mask2 = compute_epi_mask(mean_image, exclude_zeros=True, opening=False)
assert_array_equal(get_data(mask1), get_data(mask2))
mean_image2 = np.zeros((30, 30, 3))
mean_image2[3:12, 3:12, :] = get_data(mean_image)
mean_image2 = Nifti1Image(mean_image2, affine_eye)
mask3 = compute_epi_mask(mean_image2, exclude_zeros=True, opening=False)
assert_array_equal(get_data(mask1), get_data(mask3)[3:12, 3:12])
mask3 = compute_epi_mask(mean_image2, opening=False)
assert not np.allclose(get_data(mask1), get_data(mask3)[3:12, 3:12])
```

## Next Steps


---

*Source: test_masking.py:214 | Complexity: Advanced | Last updated: 2026-05-18*