# How To: Compute Epi Mask Errors Warnings

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that we get a ValueError for incorrect shape.

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

### Step 1: 'Check that we get a ValueError for incorrect shape.'

```python
'Check that we get a ValueError for incorrect shape.'
```

### Step 2: Assign mean_image = np.ones(...)

```python
mean_image = np.ones((9, 9))
```

### Step 3: Assign unknown = 10

```python
mean_image[3:-3, 3:-3] = 10
```

### Step 4: Assign unknown = 100

```python
mean_image[5, 5] = 100
```

### Step 5: Assign mean_image = Nifti1Image(...)

```python
mean_image = Nifti1Image(mean_image, affine_eye)
```

### Step 6: Assign mean_image = np.zeros(...)

```python
mean_image = np.zeros((9, 9, 9))
```

### Step 7: Assign unknown = value

```python
mean_image[0, 0, 1] = -1
```

### Step 8: Assign unknown = 1.2

```python
mean_image[0, 0, 0] = 1.2
```

### Step 9: Assign unknown = 1.1

```python
mean_image[0, 0, 2] = 1.1
```

### Step 10: Assign mean_image = Nifti1Image(...)

```python
mean_image = Nifti1Image(mean_image, affine_eye)
```

### Step 11: Call compute_epi_mask()

```python
compute_epi_mask(mean_image)
```

### Step 12: Call compute_epi_mask()

```python
compute_epi_mask(mean_image, exclude_zeros=True)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Check that we get a ValueError for incorrect shape.'
mean_image = np.ones((9, 9))
mean_image[3:-3, 3:-3] = 10
mean_image[5, 5] = 100
mean_image = Nifti1Image(mean_image, affine_eye)
with pytest.raises(ValueError, match='Computation expects 3D or 4D images, but 2 dimensions were given'):
    compute_epi_mask(mean_image)
mean_image = np.zeros((9, 9, 9))
mean_image[0, 0, 1] = -1
mean_image[0, 0, 0] = 1.2
mean_image[0, 0, 2] = 1.1
mean_image = Nifti1Image(mean_image, affine_eye)
with pytest.warns(MaskWarning, match='Computed an empty mask'):
    compute_epi_mask(mean_image, exclude_zeros=True)
```

## Next Steps


---

*Source: test_masking.py:242 | Complexity: Advanced | Last updated: 2026-05-18*