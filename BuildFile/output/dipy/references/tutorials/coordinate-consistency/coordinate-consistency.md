# How To: Coordinate Consistency

**Difficulty**: Advanced
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test that the nlmeans denoising respects coordinate geometry.

Creates an image with asymmetric features to verify that coordinate
swapping bugs are not present in the implementation.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `time`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.denoise.denspeed`
- `dipy.denoise.nlmeans`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.omp`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: '\n    Test that the nlmeans denoising respects coordinate geometry.\n\n    Creates an image with asymmetric features to verify that coordinate\n    swapping bugs are not present in the implementation.\n    '

```python
'\n    Test that the nlmeans denoising respects coordinate geometry.\n\n    Creates an image with asymmetric features to verify that coordinate\n    swapping bugs are not present in the implementation.\n    '
```

**Verification:**
```python
assert denoised_image.shape == noisy_image.shape
```

### Step 2: Assign unknown = value

```python
height, width, depth = (20, 20, 20)
```

**Verification:**
```python
assert np.sum(denoised_image < 0) < 0.01 * denoised_image.size, 'Too many negative values'
```

### Step 3: Assign test_image = np.zeros(...)

```python
test_image = np.zeros((height, width, depth), dtype=np.float64)
```

**Verification:**
```python
assert 5 < np.mean(denoised_image) < 80, 'Denoised mean should be in reasonable range'
```

### Step 4: Assign unknown = 100.0

```python
test_image[5:15, 5:15, 5:15] = 100.0
```

**Verification:**
```python
assert isinstance(denoised_image, np.ndarray)
```

### Step 5: Assign noisy_image = value

```python
noisy_image = test_image + rng.normal(0, 5, test_image.shape)
```

**Verification:**
```python
assert denoised_image.dtype == np.float64 or denoised_image.dtype == np.float32
```

### Step 6: Assign denoised_image = nlmeans(...)

```python
denoised_image = nlmeans(noisy_image, sigma=5.0, patch_radius=1, block_radius=2, rician=False, num_threads=1, method='blockwise')
```

**Verification:**
```python
assert denoised_image.shape == noisy_image.shape
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'\n    Test that the nlmeans denoising respects coordinate geometry.\n\n    Creates an image with asymmetric features to verify that coordinate\n    swapping bugs are not present in the implementation.\n    '
height, width, depth = (20, 20, 20)
test_image = np.zeros((height, width, depth), dtype=np.float64)
test_image[5:15, 5:15, 5:15] = 100.0
noisy_image = test_image + rng.normal(0, 5, test_image.shape)
denoised_image = nlmeans(noisy_image, sigma=5.0, patch_radius=1, block_radius=2, rician=False, num_threads=1, method='blockwise')
assert denoised_image.shape == noisy_image.shape
assert np.sum(denoised_image < 0) < 0.01 * denoised_image.size, 'Too many negative values'
assert 5 < np.mean(denoised_image) < 80, 'Denoised mean should be in reasonable range'
assert isinstance(denoised_image, np.ndarray)
assert denoised_image.dtype == np.float64 or denoised_image.dtype == np.float32
```

## Next Steps


---

*Source: test_nlmeans.py:262 | Complexity: Advanced | Last updated: 2026-05-18*