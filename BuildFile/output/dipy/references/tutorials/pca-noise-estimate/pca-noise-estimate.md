# How To: Pca Noise Estimate

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test pca noise estimate

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

### Step 1: Assign bvals1 = np.concatenate(...)

```python
bvals1 = np.concatenate([np.zeros(17), np.ones(3) * 1000])
```

**Verification:**
```python
assert_array_almost_equal(np.mean(sigma_est), sigma, decimal=1)
```

### Step 2: Assign bvecs1 = np.concatenate(...)

```python
bvecs1 = np.concatenate([np.zeros((17, 3)), np.eye(3)])
```

**Verification:**
```python
assert_(np.mean(pca_noise_estimate(data, gtab, correct_bias=True, images_as_samples=images_as_samples)) > np.mean(pca_noise_estimate(data, gtab, correct_bias=False, images_as_samples=images_as_samples)))
```

### Step 3: Assign gtab1 = dpg.gradient_table(...)

```python
gtab1 = dpg.gradient_table(bvals1, bvecs=bvecs1)
```

**Verification:**
```python
assert_warns(UserWarning, pca_noise_estimate, data, gtab, patch_radius=0)
```

### Step 4: Assign bvals2 = np.concatenate(...)

```python
bvals2 = np.concatenate([np.zeros(1), np.ones(3) * 1000])
```

### Step 5: Assign bvecs2 = np.concatenate(...)

```python
bvecs2 = np.concatenate([np.zeros((1, 3)), np.eye(3)])
```

### Step 6: Assign gtab2 = dpg.gradient_table(...)

```python
gtab2 = dpg.gradient_table(bvals2, bvecs=bvecs2)
```

### Step 7: Call assert_()

```python
assert_(np.mean(pca_noise_estimate(data, gtab, correct_bias=True, images_as_samples=images_as_samples)) > np.mean(pca_noise_estimate(data, gtab, correct_bias=False, images_as_samples=images_as_samples)))
```

### Step 8: Call assert_warns()

```python
assert_warns(UserWarning, pca_noise_estimate, data, gtab, patch_radius=0)
```

### Step 9: Assign signal = np.ones(...)

```python
signal = np.ones((20, 20, 20, gtab.bvals.shape[0]))
```

### Step 10: Assign sigma = 1

```python
sigma = 1
```

### Step 11: Assign noise1 = rng.normal(...)

```python
noise1 = rng.normal(0, sigma, size=signal.shape)
```

### Step 12: Assign noise2 = rng.normal(...)

```python
noise2 = rng.normal(0, sigma, size=signal.shape)
```

### Step 13: Assign data = np.sqrt(...)

```python
data = np.sqrt((signal + noise1) ** 2 + noise2 ** 2)
```

### Step 14: Assign sigma_est = pca_noise_estimate(...)

```python
sigma_est = pca_noise_estimate(data.astype(dtype), gtab, correct_bias=correct_bias, patch_radius=patch_radius, images_as_samples=images_as_samples)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.mean(sigma_est), sigma, decimal=1)
```

### Step 16: Assign signal = value

```python
signal = signal * 100
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
bvals1 = np.concatenate([np.zeros(17), np.ones(3) * 1000])
bvecs1 = np.concatenate([np.zeros((17, 3)), np.eye(3)])
gtab1 = dpg.gradient_table(bvals1, bvecs=bvecs1)
bvals2 = np.concatenate([np.zeros(1), np.ones(3) * 1000])
bvecs2 = np.concatenate([np.zeros((1, 3)), np.eye(3)])
gtab2 = dpg.gradient_table(bvals2, bvecs=bvecs2)
for images_as_samples in [True, False]:
    for patch_radius in [1, 2]:
        for gtab in [gtab1, gtab2]:
            for dtype in [np.int16, np.float64]:
                signal = np.ones((20, 20, 20, gtab.bvals.shape[0]))
                for correct_bias in [True, False]:
                    if not correct_bias:
                        signal = signal * 100
                    sigma = 1
                    noise1 = rng.normal(0, sigma, size=signal.shape)
                    noise2 = rng.normal(0, sigma, size=signal.shape)
                    data = np.sqrt((signal + noise1) ** 2 + noise2 ** 2)
                    sigma_est = pca_noise_estimate(data.astype(dtype), gtab, correct_bias=correct_bias, patch_radius=patch_radius, images_as_samples=images_as_samples)
                    assert_array_almost_equal(np.mean(sigma_est), sigma, decimal=1)
    assert_(np.mean(pca_noise_estimate(data, gtab, correct_bias=True, images_as_samples=images_as_samples)) > np.mean(pca_noise_estimate(data, gtab, correct_bias=False, images_as_samples=images_as_samples)))
    assert_warns(UserWarning, pca_noise_estimate, data, gtab, patch_radius=0)
```

## Next Steps


---

*Source: test_noise_estimate.py:192 | Complexity: Advanced | Last updated: 2026-05-18*