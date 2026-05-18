# How To: Compute Background Mask

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test compute_background_mask.

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
# Fixtures: affine_eye, value
```

## Step-by-Step Guide

### Step 1: 'Test compute_background_mask.'

```python
'Test compute_background_mask.'
```

**Verification:**
```python
assert_array_equal(get_data(mask1), mask.astype(np.int8))
```

### Step 2: Assign mean_image = value

```python
mean_image = value * np.ones((9, 9, 9))
```

### Step 3: Assign unknown = 1

```python
mean_image[3:-3, 3:-3, 3:-3] = 1
```

### Step 4: Assign mask = value

```python
mask = mean_image == 1
```

### Step 5: Assign mean_image = Nifti1Image(...)

```python
mean_image = Nifti1Image(mean_image, affine_eye)
```

### Step 6: Assign mask1 = compute_background_mask(...)

```python
mask1 = compute_background_mask(mean_image, opening=False, verbose=1)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(get_data(mask1), mask.astype(np.int8))
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, value

# Workflow
'Test compute_background_mask.'
mean_image = value * np.ones((9, 9, 9))
mean_image[3:-3, 3:-3, 3:-3] = 1
mask = mean_image == 1
mean_image = Nifti1Image(mean_image, affine_eye)
mask1 = compute_background_mask(mean_image, opening=False, verbose=1)
assert_array_equal(get_data(mask1), mask.astype(np.int8))
```

## Next Steps


---

*Source: test_masking.py:269 | Complexity: Intermediate | Last updated: 2026-05-18*