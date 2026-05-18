# How To: Ascm Accuracy

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test ascm accuracy

## Prerequisites

**Required Modules:**
- `nibabel`
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.denoise.adaptive_soft_matching`
- `dipy.denoise.nlmeans`
- `dipy.denoise.noise_estimate`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign f_name = dpd.get_fnames(...)

```python
f_name = dpd.get_fnames(name='ascm_test')
```

**Verification:**
```python
assert_(correlation > 0.9)
```

### Step 2: Assign test_ascm_data_ref = np.asanyarray(...)

```python
test_ascm_data_ref = np.asanyarray(nib.load(f_name).dataobj)
```

**Verification:**
```python
assert_(mean_diff < 10.0)
```

### Step 3: Assign test_data = np.asanyarray(...)

```python
test_data = np.asanyarray(nib.load(dpd.get_fnames(name='aniso_vox')).dataobj)
```

**Verification:**
```python
assert_(np.var(S0n_masked) < np.var(orig_masked))
```

### Step 4: Assign mask = value

```python
mask = test_data > 50
```

### Step 5: Assign sigma = estimate_sigma.item(...)

```python
sigma = estimate_sigma(test_data, N=4).item()
```

### Step 6: Assign den_small = nlmeans(...)

```python
den_small = nlmeans(test_data, sigma=sigma, mask=mask, patch_radius=1, block_radius=1, rician=True)
```

### Step 7: Assign den_large = nlmeans(...)

```python
den_large = nlmeans(test_data, sigma=sigma, mask=mask, patch_radius=2, block_radius=1, rician=True)
```

### Step 8: Assign S0n = np.array(...)

```python
S0n = np.array(adaptive_soft_matching(test_data, den_small, den_large, sigma))
```

### Step 9: Assign S0n_masked = value

```python
S0n_masked = S0n[mask]
```

### Step 10: Assign ref_masked = value

```python
ref_masked = test_ascm_data_ref[mask]
```

### Step 11: Assign orig_masked = value

```python
orig_masked = test_data[mask]
```

### Step 12: Assign correlation = value

```python
correlation = np.corrcoef(S0n_masked.flatten(), ref_masked.flatten())[0, 1]
```

### Step 13: Call assert_()

```python
assert_(correlation > 0.9)
```

### Step 14: Assign mean_diff = np.abs(...)

```python
mean_diff = np.abs(np.mean(S0n_masked) - np.mean(ref_masked))
```

### Step 15: Call assert_()

```python
assert_(mean_diff < 10.0)
```

### Step 16: Call assert_()

```python
assert_(np.var(S0n_masked) < np.var(orig_masked))
```


## Complete Example

```python
# Workflow
f_name = dpd.get_fnames(name='ascm_test')
test_ascm_data_ref = np.asanyarray(nib.load(f_name).dataobj)
test_data = np.asanyarray(nib.load(dpd.get_fnames(name='aniso_vox')).dataobj)
mask = test_data > 50
sigma = estimate_sigma(test_data, N=4).item()
den_small = nlmeans(test_data, sigma=sigma, mask=mask, patch_radius=1, block_radius=1, rician=True)
den_large = nlmeans(test_data, sigma=sigma, mask=mask, patch_radius=2, block_radius=1, rician=True)
S0n = np.array(adaptive_soft_matching(test_data, den_small, den_large, sigma))
S0n_masked = S0n[mask]
ref_masked = test_ascm_data_ref[mask]
orig_masked = test_data[mask]
correlation = np.corrcoef(S0n_masked.flatten(), ref_masked.flatten())[0, 1]
assert_(correlation > 0.9)
mean_diff = np.abs(np.mean(S0n_masked) - np.mean(ref_masked))
assert_(mean_diff < 10.0)
assert_(np.var(S0n_masked) < np.var(orig_masked))
```

## Next Steps


---

*Source: test_ascm.py:91 | Complexity: Advanced | Last updated: 2026-05-18*