# How To: Compute Background Mask Errors Warnings

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
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

### Step 7: Assign mean_image = Nifti1Image(...)

```python
mean_image = Nifti1Image(mean_image, affine_eye)
```

### Step 8: Call compute_background_mask()

```python
compute_background_mask(mean_image)
```

### Step 9: Call compute_background_mask()

```python
compute_background_mask(mean_image)
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
with pytest.raises(ValueError):
    compute_background_mask(mean_image)
mean_image = np.zeros((9, 9, 9))
mean_image = Nifti1Image(mean_image, affine_eye)
with pytest.warns(MaskWarning, match='Computed an empty mask'):
    compute_background_mask(mean_image)
```

## Next Steps


---

*Source: test_masking.py:281 | Complexity: Advanced | Last updated: 2026-05-18*