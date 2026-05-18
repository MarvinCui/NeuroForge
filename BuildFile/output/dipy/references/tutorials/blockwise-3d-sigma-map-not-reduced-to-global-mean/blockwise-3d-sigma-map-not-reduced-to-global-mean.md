# How To: Blockwise 3D Sigma Map Not Reduced To Global Mean

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Blockwise 3D sigma maps should affect denoising beyond a global mean.

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

### Step 1: 'Blockwise 3D sigma maps should affect denoising beyond a global mean.'

```python
'Blockwise 3D sigma maps should affect denoising beyond a global mean.'
```

**Verification:**
```python
assert result_map.shape == arr.shape
```

### Step 2: Assign arr = rng.normal.astype(...)

```python
arr = rng.normal(100, 15, size=(10, 10, 10)).astype(np.float64)
```

**Verification:**
```python
assert result_scalar.shape == arr.shape
```

### Step 3: Assign sigma_map = np.ones(...)

```python
sigma_map = np.ones(arr.shape, dtype=np.float64)
```

**Verification:**
```python
assert np.max(np.abs(result_map - result_scalar)) > 1e-06
```

### Step 4: Assign unknown = 2.0

```python
sigma_map[:5, :, :] = 2.0
```

### Step 5: Assign unknown = 20.0

```python
sigma_map[5:, :, :] = 20.0
```

### Step 6: Assign result_map = nlmeans(...)

```python
result_map = nlmeans(arr, sigma=sigma_map, method='blockwise', rician=False, num_threads=1)
```

### Step 7: Assign result_scalar = nlmeans(...)

```python
result_scalar = nlmeans(arr, sigma=float(np.mean(sigma_map)), method='blockwise', rician=False, num_threads=1)
```

**Verification:**
```python
assert result_map.shape == arr.shape
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Blockwise 3D sigma maps should affect denoising beyond a global mean.'
arr = rng.normal(100, 15, size=(10, 10, 10)).astype(np.float64)
sigma_map = np.ones(arr.shape, dtype=np.float64)
sigma_map[:5, :, :] = 2.0
sigma_map[5:, :, :] = 20.0
result_map = nlmeans(arr, sigma=sigma_map, method='blockwise', rician=False, num_threads=1)
result_scalar = nlmeans(arr, sigma=float(np.mean(sigma_map)), method='blockwise', rician=False, num_threads=1)
assert result_map.shape == arr.shape
assert result_scalar.shape == arr.shape
assert np.max(np.abs(result_map - result_scalar)) > 1e-06
```

## Next Steps


---

*Source: test_nlmeans.py:233 | Complexity: Intermediate | Last updated: 2026-05-18*