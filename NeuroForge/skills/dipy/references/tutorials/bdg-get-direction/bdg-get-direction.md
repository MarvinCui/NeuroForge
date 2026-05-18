# How To: Bdg Get Direction

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: This tests the direction found by the bootstrap direction getter.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction.bootstrap_direction_getter`
- `dipy.io.gradients`
- `dipy.reconst`
- `dipy.reconst.csdeconv`
- `dipy.sims.voxel`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: 'This tests the direction found by the bootstrap direction getter.'

```python
'This tests the direction found by the bootstrap direction getter.'
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
gtab = gradient_table(bvals, bvecs=bvecs, b0_threshold=0)
```

### Step 5: Assign mevals = np.array(...)

```python
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
```

### Step 6: Assign angles = value

```python
angles = [(0, 0)]
```

### Step 7: Assign unknown = multi_tensor(...)

```python
voxel, _ = multi_tensor(gtab, mevals, S0=1, angles=angles, fractions=[100], snr=100)
```

### Step 8: Assign data = np.tile(...)

```python
data = np.tile(voxel, (3, 3, 3, 1))
```

### Step 9: Assign sphere = get_sphere(...)

```python
sphere = get_sphere(name='symmetric362')
```

### Step 10: Assign response = value

```python
response = (np.array([0.0015, 0.0003, 0.0003]), 1)
```

### Step 11: Assign point = np.array(...)

```python
point = np.array([0.0, 0.0, 0.0])
```

### Step 12: Assign prev_direction = value

```python
prev_direction = sphere.vertices[5]
```

### Step 13: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 14: Assign csd_model = ConstrainedSphericalDeconvModel(...)

```python
csd_model = ConstrainedSphericalDeconvModel(gtab, response, sh_order_max=6)
```

### Step 15: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 16: Assign boot_dg = BootDirectionGetter(...)

```python
boot_dg = BootDirectionGetter(data, model=csd_model, max_angle=10.0, sphere=sphere)
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(boot_dg.get_direction(point, prev_direction), 1)
```

### Step 18: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 19: Assign boot_dg = BootDirectionGetter(...)

```python
boot_dg = BootDirectionGetter(data, model=csd_model, max_angle=10, sphere=sphere, max_attempts=3)
```

### Step 20: Call npt.assert_equal()

```python
npt.assert_equal(boot_dg.get_direction(point, prev_direction), 1)
```

### Step 21: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 22: Assign boot_dg = BootDirectionGetter(...)

```python
boot_dg = BootDirectionGetter(data, model=csd_model, max_angle=60.0, sphere=sphere, max_attempts=5)
```

### Step 23: Call npt.assert_equal()

```python
npt.assert_equal(boot_dg.get_direction(point, prev_direction), 0)
```

### Step 24: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 25: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, lambda: BootDirectionGetter(data, csd_model, 60, sphere=sphere, max_attempts=0))
```


## Complete Example

```python
# Workflow
'This tests the direction found by the bootstrap direction getter.'
_, fbvals, fbvecs = get_fnames(name='small_64D')
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
gtab = gradient_table(bvals, bvecs=bvecs, b0_threshold=0)
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
angles = [(0, 0)]
voxel, _ = multi_tensor(gtab, mevals, S0=1, angles=angles, fractions=[100], snr=100)
data = np.tile(voxel, (3, 3, 3, 1))
sphere = get_sphere(name='symmetric362')
response = (np.array([0.0015, 0.0003, 0.0003]), 1)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    csd_model = ConstrainedSphericalDeconvModel(gtab, response, sh_order_max=6)
point = np.array([0.0, 0.0, 0.0])
prev_direction = sphere.vertices[5]
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    boot_dg = BootDirectionGetter(data, model=csd_model, max_angle=10.0, sphere=sphere)
    npt.assert_equal(boot_dg.get_direction(point, prev_direction), 1)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    boot_dg = BootDirectionGetter(data, model=csd_model, max_angle=10, sphere=sphere, max_attempts=3)
    npt.assert_equal(boot_dg.get_direction(point, prev_direction), 1)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    boot_dg = BootDirectionGetter(data, model=csd_model, max_angle=60.0, sphere=sphere, max_attempts=5)
    npt.assert_equal(boot_dg.get_direction(point, prev_direction), 0)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    npt.assert_raises(ValueError, lambda: BootDirectionGetter(data, csd_model, 60, sphere=sphere, max_attempts=0))
```

## Next Steps


---

*Source: test_bootstrap_direction_getter.py:73 | Complexity: Advanced | Last updated: 2026-05-18*