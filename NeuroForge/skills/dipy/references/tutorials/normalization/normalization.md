# How To: Normalization

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the normalization routine applied after a convolution

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.denoise.enhancement_kernel`
- `dipy.denoise.shift_twist_convolution`
- `dipy.reconst.shm`


## Step-by-Step Guide

### Step 1: 'Test the normalization routine applied after a convolution'

```python
'Test the normalization routine applied after a convolution'
```

### Step 2: Assign D33 = 1.0

```python
D33 = 1.0
```

### Step 3: Assign D44 = 0.04

```python
D44 = 0.04
```

### Step 4: Assign t = 1

```python
t = 1
```

### Step 5: Assign num_orientations = 5

```python
num_orientations = 5
```

### Step 6: Assign k = EnhancementKernel(...)

```python
k = EnhancementKernel(D33, D44, t, orientations=num_orientations, force_recompute=True)
```

### Step 7: Assign numorientations = value

```python
numorientations = k.get_orientations().shape[0]
```

### Step 8: Assign spike = np.ones(...)

```python
spike = np.ones((7, 7, 7, numorientations), dtype=np.float64)
```

### Step 9: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(np.amax(csd_enh_dsf), np.amax(spike))
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 11: Assign spike_sh = sf_to_sh(...)

```python
spike_sh = sf_to_sh(spike, k.get_sphere(), sh_order_max=8)
```

### Step 12: Assign csd_enh = convolve(...)

```python
csd_enh = convolve(spike_sh, k, sh_order_max=8, test_mode=True, normalize=True)
```

### Step 13: Assign csd_enh_dsf = sh_to_sf(...)

```python
csd_enh_dsf = sh_to_sf(csd_enh, k.get_sphere(), sh_order_max=8, basis_type=None)
```


## Complete Example

```python
# Workflow
'Test the normalization routine applied after a convolution'
D33 = 1.0
D44 = 0.04
t = 1
num_orientations = 5
k = EnhancementKernel(D33, D44, t, orientations=num_orientations, force_recompute=True)
numorientations = k.get_orientations().shape[0]
spike = np.ones((7, 7, 7, numorientations), dtype=np.float64)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    spike_sh = sf_to_sh(spike, k.get_sphere(), sh_order_max=8)
    csd_enh = convolve(spike_sh, k, sh_order_max=8, test_mode=True, normalize=True)
    csd_enh_dsf = sh_to_sf(csd_enh, k.get_sphere(), sh_order_max=8, basis_type=None)
npt.assert_almost_equal(np.amax(csd_enh_dsf), np.amax(spike))
```

## Next Steps


---

*Source: test_kernel.py:119 | Complexity: Advanced | Last updated: 2026-05-18*