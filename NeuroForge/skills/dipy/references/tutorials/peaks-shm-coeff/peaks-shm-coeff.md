# How To: Peaks Shm Coeff

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test peaks shm coeff

## Prerequisites

**Required Modules:**
- `io`
- `pickle`
- `random`
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.direction.pmf`
- `dipy.io.gradients`
- `dipy.reconst.odf`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking.utils`


## Step-by-Step Guide

### Step 1: Assign SNR = 100

```python
SNR = 100
```

**Verification:**
```python
assert_array_almost_equal(pam.odf, odf2)
```

### Step 2: Assign S0 = 100

```python
S0 = 100
```

**Verification:**
```python
assert_equal(pam.shm_coeff.shape[-1], 45)
```

### Step 3: Assign unknown = get_fnames(...)

```python
_, fbvals, fbvecs = get_fnames(name='small_64D')
```

**Verification:**
```python
assert_equal(pam.shm_coeff, None)
```

### Step 4: Assign sphere = default_sphere

```python
sphere = default_sphere
```

**Verification:**
```python
assert_array_almost_equal(pam.odf, odf2)
```

### Step 5: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
```

### Step 6: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 7: Assign mevals = np.array(...)

```python
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
```

### Step 8: Assign unknown = multi_tensor(...)

```python
data, _ = multi_tensor(gtab, mevals, S0=S0, angles=[(0, 0), (60, 0)], fractions=[50, 50], snr=SNR)
```

### Step 9: Assign odf2 = np.dot(...)

```python
odf2 = np.dot(pam.shm_coeff, pam.B)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pam.odf, odf2)
```

### Step 11: Call assert_equal()

```python
assert_equal(pam.shm_coeff.shape[-1], 45)
```

### Step 12: Call assert_equal()

```python
assert_equal(pam.shm_coeff, None)
```

### Step 13: Assign odf2 = np.dot(...)

```python
odf2 = np.dot(pam.shm_coeff, pam.B)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pam.odf, odf2)
```

### Step 15: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 16: Assign model = CsaOdfModel(...)

```python
model = CsaOdfModel(gtab, 4)
```

### Step 17: Assign pam = peaks_from_model(...)

```python
pam = peaks_from_model(model, data[None, :], sphere, 0.5, 45, return_odf=True, return_sh=True)
```

### Step 18: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 19: Assign pam = peaks_from_model(...)

```python
pam = peaks_from_model(model, data[None, :], sphere, 0.5, 45, return_odf=True, return_sh=False)
```

### Step 20: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=tournier07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 21: Assign pam = peaks_from_model(...)

```python
pam = peaks_from_model(model, data[None, :], sphere, 0.5, 45, return_odf=True, return_sh=True, sh_basis_type='tournier07')
```


## Complete Example

```python
# Workflow
SNR = 100
S0 = 100
_, fbvals, fbvecs = get_fnames(name='small_64D')
sphere = default_sphere
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
gtab = gradient_table(bvals, bvecs=bvecs)
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
data, _ = multi_tensor(gtab, mevals, S0=S0, angles=[(0, 0), (60, 0)], fractions=[50, 50], snr=SNR)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model = CsaOdfModel(gtab, 4)
    pam = peaks_from_model(model, data[None, :], sphere, 0.5, 45, return_odf=True, return_sh=True)
odf2 = np.dot(pam.shm_coeff, pam.B)
assert_array_almost_equal(pam.odf, odf2)
assert_equal(pam.shm_coeff.shape[-1], 45)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    pam = peaks_from_model(model, data[None, :], sphere, 0.5, 45, return_odf=True, return_sh=False)
assert_equal(pam.shm_coeff, None)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=tournier07_legacy_msg, category=PendingDeprecationWarning)
    pam = peaks_from_model(model, data[None, :], sphere, 0.5, 45, return_odf=True, return_sh=True, sh_basis_type='tournier07')
odf2 = np.dot(pam.shm_coeff, pam.B)
assert_array_almost_equal(pam.odf, odf2)
```

## Next Steps


---

*Source: test_peaks.py:728 | Complexity: Advanced | Last updated: 2026-05-18*