# How To: Sphere Scaling Csdmodel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that mirroring regularization sphere does not change the result of
the model

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.io.gradients`
- `dipy.reconst.csdeconv`
- `dipy.reconst.dti`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: 'Check that mirroring regularization sphere does not change the result of\n    the model'

```python
'Check that mirroring regularization sphere does not change the result of\n    the model'
```

**Verification:**
```python
assert_array_almost_equal(csd_fit_full.shm_coeff, csd_fit_hemi.shm_coeff)
```

### Step 2: Assign unknown = get_fnames(...)

```python
_, fbvals, fbvecs = get_fnames(name='small_64D')
```

### Step 3: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
```

### Step 4: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 5: Assign mevals = np.array(...)

```python
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
```

### Step 6: Assign angles = value

```python
angles = [(0, 0), (60, 0)]
```

### Step 7: Assign unknown = multi_tensor(...)

```python
S, _ = multi_tensor(gtab, mevals, S0=100.0, angles=angles, fractions=[50, 50], snr=None)
```

### Step 8: Assign hemi = small_sphere

```python
hemi = small_sphere
```

### Step 9: Assign sphere = hemi.mirror(...)

```python
sphere = hemi.mirror()
```

### Step 10: Assign response = value

```python
response = (np.array([0.0015, 0.0003, 0.0003]), 100)
```

### Step 11: Assign csd_fit_full = model_full.fit(...)

```python
csd_fit_full = model_full.fit(S)
```

### Step 12: Assign csd_fit_hemi = model_hemi.fit(...)

```python
csd_fit_hemi = model_hemi.fit(S)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(csd_fit_full.shm_coeff, csd_fit_hemi.shm_coeff)
```

### Step 14: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 15: Assign model_full = ConstrainedSphericalDeconvModel(...)

```python
model_full = ConstrainedSphericalDeconvModel(gtab, response, reg_sphere=sphere)
```

### Step 16: Assign model_hemi = ConstrainedSphericalDeconvModel(...)

```python
model_hemi = ConstrainedSphericalDeconvModel(gtab, response, reg_sphere=hemi)
```


## Complete Example

```python
# Workflow
'Check that mirroring regularization sphere does not change the result of\n    the model'
_, fbvals, fbvecs = get_fnames(name='small_64D')
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
gtab = gradient_table(bvals, bvecs=bvecs)
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
angles = [(0, 0), (60, 0)]
S, _ = multi_tensor(gtab, mevals, S0=100.0, angles=angles, fractions=[50, 50], snr=None)
hemi = small_sphere
sphere = hemi.mirror()
response = (np.array([0.0015, 0.0003, 0.0003]), 100)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model_full = ConstrainedSphericalDeconvModel(gtab, response, reg_sphere=sphere)
    model_hemi = ConstrainedSphericalDeconvModel(gtab, response, reg_sphere=hemi)
csd_fit_full = model_full.fit(S)
csd_fit_hemi = model_hemi.fit(S)
assert_array_almost_equal(csd_fit_full.shm_coeff, csd_fit_hemi.shm_coeff)
```

## Next Steps


---

*Source: test_csdeconv.py:686 | Complexity: Advanced | Last updated: 2026-05-18*