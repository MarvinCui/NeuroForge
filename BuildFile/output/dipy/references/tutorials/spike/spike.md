# How To: Spike

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if a convolution with a delta spike is equal to the kernel
saved in the lookup table.

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

### Step 1: 'Test if a convolution with a delta spike is equal to the kernel\n    saved in the lookup table.'

```python
'Test if a convolution with a delta spike is equal to the kernel\n    saved in the lookup table.'
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

### Step 8: Assign spike = np.zeros(...)

```python
spike = np.zeros((7, 7, 7, numorientations), dtype=np.float64)
```

### Step 9: Assign unknown = 1

```python
spike[3, 3, 3, 0] = 1
```

### Step 10: Assign csd_enh = convolve_sf(...)

```python
csd_enh = convolve_sf(spike, k, test_mode=True, normalize=False)
```

### Step 11: Assign totalsum = 0.0

```python
totalsum = 0.0
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(totalsum, 0.0)
```


## Complete Example

```python
# Workflow
'Test if a convolution with a delta spike is equal to the kernel\n    saved in the lookup table.'
D33 = 1.0
D44 = 0.04
t = 1
num_orientations = 5
k = EnhancementKernel(D33, D44, t, orientations=num_orientations, force_recompute=True)
numorientations = k.get_orientations().shape[0]
spike = np.zeros((7, 7, 7, numorientations), dtype=np.float64)
spike[3, 3, 3, 0] = 1
csd_enh = convolve_sf(spike, k, test_mode=True, normalize=False)
totalsum = 0.0
for i in range(0, numorientations):
    totalsum += np.sum(np.array(k.get_lookup_table())[i, 0, :, :, :] - np.array(csd_enh)[:, :, :, i])
npt.assert_equal(totalsum, 0.0)
```

## Next Steps


---

*Source: test_kernel.py:88 | Complexity: Advanced | Last updated: 2026-05-18*