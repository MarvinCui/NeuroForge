# How To: Piesno

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test piesno

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.denoise.noise_estimate`
- `dipy.denoise.pca_noise_estimate`
- `dipy.io.image`
- `dipy.testing`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign test_piesno_data = load_nifti_data(...)

```python
test_piesno_data = load_nifti_data(dpd.get_fnames(name='test_piesno'))
```

**Verification:**
```python
assert_almost_equal(sigma, 0.010749458025559)
```

### Step 2: Assign sigma = piesno(...)

```python
sigma = piesno(test_piesno_data, N=8, alpha=0.01, step=1, eps=1e-10, return_mask=False)
```

**Verification:**
```python
assert_(np.abs(sigma - 50) / sigma < 0.03)
```

### Step 3: Call assert_almost_equal()

```python
assert_almost_equal(sigma, 0.010749458025559)
```

**Verification:**
```python
assert_(np.abs(sigma - 50) / sigma < 0.03)
```

### Step 4: Assign noise1 = value

```python
noise1 = rng.standard_normal((100, 100, 100)) * 50 + 10
```

**Verification:**
```python
assert_(np.abs(sigma - 50) / sigma < 0.03)
```

### Step 5: Assign noise2 = value

```python
noise2 = rng.standard_normal((100, 100, 100)) * 50 + 10
```

**Verification:**
```python
assert_(np.all(sigma == 0))
```

### Step 6: Assign rician_noise = np.sqrt(...)

```python
rician_noise = np.sqrt(noise1 ** 2 + noise2 ** 2)
```

**Verification:**
```python
assert_(np.all(sigma == 0))
```

### Step 7: Assign unknown = piesno(...)

```python
sigma, mask = piesno(rician_noise, N=1, alpha=0.01, step=1, eps=1e-10, return_mask=True)
```

**Verification:**
```python
assert_(np.all(mask == 0))
```

### Step 8: Call assert_()

```python
assert_(np.abs(sigma - 50) / sigma < 0.03)
```

**Verification:**
```python
assert_(np.all(sigma == 10))
```

### Step 9: Assign initial_estimation = value

```python
initial_estimation = np.median(sigma) / np.sqrt(2 * _inv_nchi_cdf(1, 1, 0.5))
```

### Step 10: Assign unknown = _piesno_3D(...)

```python
sigma, mask = _piesno_3D(rician_noise, N=1, alpha=0.01, step=1, eps=1e-10, return_mask=True, initial_estimation=initial_estimation)
```

### Step 11: Call assert_()

```python
assert_(np.abs(sigma - 50) / sigma < 0.03)
```

### Step 12: Assign sigma = _piesno_3D(...)

```python
sigma = _piesno_3D(rician_noise, N=1, alpha=0.01, step=1, eps=1e-10, return_mask=False, initial_estimation=initial_estimation)
```

### Step 13: Call assert_()

```python
assert_(np.abs(sigma - 50) / sigma < 0.03)
```

### Step 14: Assign sigma = _piesno_3D(...)

```python
sigma = _piesno_3D(np.zeros_like(rician_noise), N=1, alpha=0.01, step=1, eps=1e-10, return_mask=False, initial_estimation=initial_estimation)
```

### Step 15: Call assert_()

```python
assert_(np.all(sigma == 0))
```

### Step 16: Assign unknown = _piesno_3D(...)

```python
sigma, mask = _piesno_3D(np.zeros_like(rician_noise), N=1, alpha=0.01, step=1, eps=1e-10, return_mask=True, initial_estimation=initial_estimation)
```

### Step 17: Call assert_()

```python
assert_(np.all(sigma == 0))
```

### Step 18: Call assert_()

```python
assert_(np.all(mask == 0))
```

### Step 19: Assign sigma = _piesno_3D(...)

```python
sigma = _piesno_3D(1000 * np.ones_like(rician_noise), N=1, alpha=0.01, step=1, eps=1e-10, return_mask=False, initial_estimation=10)
```

### Step 20: Call assert_()

```python
assert_(np.all(sigma == 10))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
test_piesno_data = load_nifti_data(dpd.get_fnames(name='test_piesno'))
sigma = piesno(test_piesno_data, N=8, alpha=0.01, step=1, eps=1e-10, return_mask=False)
assert_almost_equal(sigma, 0.010749458025559)
noise1 = rng.standard_normal((100, 100, 100)) * 50 + 10
noise2 = rng.standard_normal((100, 100, 100)) * 50 + 10
rician_noise = np.sqrt(noise1 ** 2 + noise2 ** 2)
sigma, mask = piesno(rician_noise, N=1, alpha=0.01, step=1, eps=1e-10, return_mask=True)
assert_(np.abs(sigma - 50) / sigma < 0.03)
initial_estimation = np.median(sigma) / np.sqrt(2 * _inv_nchi_cdf(1, 1, 0.5))
sigma, mask = _piesno_3D(rician_noise, N=1, alpha=0.01, step=1, eps=1e-10, return_mask=True, initial_estimation=initial_estimation)
assert_(np.abs(sigma - 50) / sigma < 0.03)
sigma = _piesno_3D(rician_noise, N=1, alpha=0.01, step=1, eps=1e-10, return_mask=False, initial_estimation=initial_estimation)
assert_(np.abs(sigma - 50) / sigma < 0.03)
sigma = _piesno_3D(np.zeros_like(rician_noise), N=1, alpha=0.01, step=1, eps=1e-10, return_mask=False, initial_estimation=initial_estimation)
assert_(np.all(sigma == 0))
sigma, mask = _piesno_3D(np.zeros_like(rician_noise), N=1, alpha=0.01, step=1, eps=1e-10, return_mask=True, initial_estimation=initial_estimation)
assert_(np.all(sigma == 0))
assert_(np.all(mask == 0))
sigma = _piesno_3D(1000 * np.ones_like(rician_noise), N=1, alpha=0.01, step=1, eps=1e-10, return_mask=False, initial_estimation=10)
assert_(np.all(sigma == 10))
```

## Next Steps


---

*Source: test_noise_estimate.py:39 | Complexity: Advanced | Last updated: 2026-05-18*