# How To: Generate Kernel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test generate kernel

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.core.sphere_stats`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst.csdeconv`
- `dipy.reconst.rumba`
- `dipy.reconst.shm`
- `dipy.reconst.tests.test_dsi`
- `dipy.sims.voxel`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign sphere = default_sphere

```python
sphere = default_sphere
```

**Verification:**
```python
assert_equal(kernel.shape, (len(gtab.bvals), len(sphere.vertices) + 2))
```

### Step 2: Assign btable = np.loadtxt(...)

```python
btable = np.loadtxt(get_fnames(name='dsi515btable'))
```

**Verification:**
```python
assert_almost_equal(kernel[:, 0], S)
```

### Step 3: Assign bvals = value

```python
bvals = btable[:, 0]
```

**Verification:**
```python
assert_equal(kernel.shape, (len(gtab.bvals), len(sphere.vertices) + 2))
```

### Step 4: Assign bvecs = value

```python
bvecs = btable[:, 1:]
```

**Verification:**
```python
assert_almost_equal(kernel, kernel_multi)
```

### Step 5: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

**Verification:**
```python
assert_array_equal(kernel[:, -2], np.zeros(len(gtab.bvals)))
```

### Step 6: Assign wm_response = np.array(...)

```python
wm_response = np.array([0.0017, 0.0002, 0.0002])
```

**Verification:**
```python
assert_array_equal(kernel[:, -1], np.zeros(len(gtab.bvals)))
```

### Step 7: Assign gm_response = 2e-05

```python
gm_response = 2e-05
```

### Step 8: Assign csf_response = 0.003

```python
csf_response = 0.003
```

### Step 9: Assign kernel = generate_kernel(...)

```python
kernel = generate_kernel(gtab, sphere, wm_response, gm_response, csf_response)
```

### Step 10: Call assert_equal()

```python
assert_equal(kernel.shape, (len(gtab.bvals), len(sphere.vertices) + 2))
```

### Step 11: Assign unknown = cart2sphere(...)

```python
_, theta, phi = cart2sphere(sphere.x, sphere.y, sphere.z)
```

### Step 12: Assign S0 = 1

```python
S0 = 1
```

### Step 13: Assign fi = 100

```python
fi = 100
```

### Step 14: Assign unknown = multi_tensor(...)

```python
S, _ = multi_tensor(gtab, np.array([wm_response]), S0=S0, angles=[[theta[0] * 180 / np.pi, phi[0] * 180 / np.pi]], fractions=[fi], snr=None)
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(kernel[:, 0], S)
```

### Step 16: Assign ms_eigenval_count = value

```python
ms_eigenval_count = len(unique_bvals_tolerance(gtab.bvals)) - 1
```

### Step 17: Assign wm_response_multi = np.tile(...)

```python
wm_response_multi = np.tile(wm_response, (ms_eigenval_count, 1))
```

### Step 18: Assign kernel_multi = generate_kernel(...)

```python
kernel_multi = generate_kernel(gtab, sphere, wm_response_multi, gm_response, csf_response)
```

### Step 19: Call assert_equal()

```python
assert_equal(kernel.shape, (len(gtab.bvals), len(sphere.vertices) + 2))
```

### Step 20: Call assert_almost_equal()

```python
assert_almost_equal(kernel, kernel_multi)
```

### Step 21: Assign kernel = generate_kernel(...)

```python
kernel = generate_kernel(gtab, sphere, wm_response, gm_response=None, csf_response=None)
```

### Step 22: Call assert_array_equal()

```python
assert_array_equal(kernel[:, -2], np.zeros(len(gtab.bvals)))
```

### Step 23: Call assert_array_equal()

```python
assert_array_equal(kernel[:, -1], np.zeros(len(gtab.bvals)))
```


## Complete Example

```python
# Workflow
sphere = default_sphere
btable = np.loadtxt(get_fnames(name='dsi515btable'))
bvals = btable[:, 0]
bvecs = btable[:, 1:]
gtab = gradient_table(bvals, bvecs=bvecs)
wm_response = np.array([0.0017, 0.0002, 0.0002])
gm_response = 2e-05
csf_response = 0.003
kernel = generate_kernel(gtab, sphere, wm_response, gm_response, csf_response)
assert_equal(kernel.shape, (len(gtab.bvals), len(sphere.vertices) + 2))
_, theta, phi = cart2sphere(sphere.x, sphere.y, sphere.z)
S0 = 1
fi = 100
S, _ = multi_tensor(gtab, np.array([wm_response]), S0=S0, angles=[[theta[0] * 180 / np.pi, phi[0] * 180 / np.pi]], fractions=[fi], snr=None)
assert_almost_equal(kernel[:, 0], S)
ms_eigenval_count = len(unique_bvals_tolerance(gtab.bvals)) - 1
wm_response_multi = np.tile(wm_response, (ms_eigenval_count, 1))
kernel_multi = generate_kernel(gtab, sphere, wm_response_multi, gm_response, csf_response)
assert_equal(kernel.shape, (len(gtab.bvals), len(sphere.vertices) + 2))
assert_almost_equal(kernel, kernel_multi)
kernel = generate_kernel(gtab, sphere, wm_response, gm_response=None, csf_response=None)
assert_array_equal(kernel[:, -2], np.zeros(len(gtab.bvals)))
assert_array_equal(kernel[:, -1], np.zeros(len(gtab.bvals)))
```

## Next Steps


---

*Source: test_rumba.py:406 | Complexity: Advanced | Last updated: 2026-05-18*