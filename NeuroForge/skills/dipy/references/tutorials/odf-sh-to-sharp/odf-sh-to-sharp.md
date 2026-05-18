# How To: Odf Sh To Sharp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test odf sh to sharp

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

### Step 1: Assign SNR = None

```python
SNR = None
```

**Verification:**
```python
assert_equal(directions2.shape[0], 2)
```

### Step 2: Assign S0 = 1

```python
S0 = 1
```

### Step 3: Assign unknown = get_fnames(...)

```python
_, fbvals, fbvecs = get_fnames(name='small_64D')
```

### Step 4: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
```

### Step 5: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 6: Assign mevals = np.array(...)

```python
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
```

### Step 7: Assign unknown = multi_tensor(...)

```python
S, _ = multi_tensor(gtab, mevals, S0=S0, angles=[(10, 0), (100, 0)], fractions=[50, 50], snr=SNR)
```

### Step 8: Assign sphere = default_sphere

```python
sphere = default_sphere
```

### Step 9: Assign qbfit = qb.fit(...)

```python
qbfit = qb.fit(S)
```

### Step 10: Assign Z = np.linalg.norm(...)

```python
Z = np.linalg.norm(odf_gt)
```

### Step 11: Assign odfs_gt = np.zeros(...)

```python
odfs_gt = np.zeros((3, 1, 1, odf_gt.shape[0]))
```

### Step 12: Assign unknown = value

```python
odfs_gt[:, :, :] = odf_gt[:]
```

### Step 13: Assign unknown = peak_directions(...)

```python
directions2, _, _ = peak_directions(fodf[0, 0, 0], sphere)
```

### Step 14: Call assert_equal()

```python
assert_equal(directions2.shape[0], 2)
```

### Step 15: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 16: Assign qb = QballModel(...)

```python
qb = QballModel(gtab, sh_order_max=8, assume_normed=True)
```

### Step 17: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 18: Assign odf_gt = qbfit.odf(...)

```python
odf_gt = qbfit.odf(sphere)
```

### Step 19: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 20: Assign odfs_sh = sf_to_sh(...)

```python
odfs_sh = sf_to_sh(odfs_gt, sphere, sh_order_max=8, basis_type=None)
```

### Step 21: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 22: Assign fodf_sh = odf_sh_to_sharp(...)

```python
fodf_sh = odf_sh_to_sharp(odfs_sh, sphere, basis=None, ratio=3 / 15.0, sh_order_max=8, lambda_=1.0, tau=0.1)
```

### Step 23: Assign fodf = sh_to_sf(...)

```python
fodf = sh_to_sf(fodf_sh, sphere, sh_order_max=8, basis_type=None)
```


## Complete Example

```python
# Workflow
SNR = None
S0 = 1
_, fbvals, fbvecs = get_fnames(name='small_64D')
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
gtab = gradient_table(bvals, bvecs=bvecs)
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
S, _ = multi_tensor(gtab, mevals, S0=S0, angles=[(10, 0), (100, 0)], fractions=[50, 50], snr=SNR)
sphere = default_sphere
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    qb = QballModel(gtab, sh_order_max=8, assume_normed=True)
qbfit = qb.fit(S)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    odf_gt = qbfit.odf(sphere)
Z = np.linalg.norm(odf_gt)
odfs_gt = np.zeros((3, 1, 1, odf_gt.shape[0]))
odfs_gt[:, :, :] = odf_gt[:]
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    odfs_sh = sf_to_sh(odfs_gt, sphere, sh_order_max=8, basis_type=None)
odfs_sh /= Z
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fodf_sh = odf_sh_to_sharp(odfs_sh, sphere, basis=None, ratio=3 / 15.0, sh_order_max=8, lambda_=1.0, tau=0.1)
    fodf = sh_to_sf(fodf_sh, sphere, sh_order_max=8, basis_type=None)
directions2, _, _ = peak_directions(fodf[0, 0, 0], sphere)
assert_equal(directions2.shape[0], 2)
```

## Next Steps


---

*Source: test_csdeconv.py:404 | Complexity: Advanced | Last updated: 2026-05-18*