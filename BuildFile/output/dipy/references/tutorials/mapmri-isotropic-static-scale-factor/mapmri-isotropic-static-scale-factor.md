# How To: Mapmri Isotropic Static Scale Factor

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mapmri isotropic static scale factor

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `math`
- `platform`
- `time`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.integrate`
- `scipy.special`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst`
- `dipy.reconst.mapmri`
- `dipy.reconst.odf`
- `dipy.reconst.shm`
- `dipy.reconst.tests.test_dsi`
- `dipy.sims.voxel`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: radial_order, rng
```

## Step-by-Step Guide

### Step 1: Assign gtab = get_gtab_taiwan_dsi(...)

```python
gtab = get_gtab_taiwan_dsi()
```

**Verification:**
```python
assert_equal(np.all(mapf_scale_stat_reg_stat.mu == mu), True)
```

### Step 2: Assign D = 0.0007

```python
D = 0.0007
```

**Verification:**
```python
assert_equal(time_scale_stat_reg_stat < time_scale_adapt_reg_stat, True, f'mapf_scale_stat_reg_stat ({time_scale_stat_reg_stat}s) slower than mapf_scale_adapt_reg_stat ({time_scale_adapt_reg_stat}s). It should be the opposite.')
```

### Step 3: Assign tau = value

```python
tau = 1 / (4 * np.pi ** 2)
```

**Verification:**
```python
assert_almost_equal(mapf_scale_stat_reg_stat.fitted_signal(), mapf_scale_adapt_reg_stat.fitted_signal())
```

### Step 4: Assign mu = np.sqrt(...)

```python
mu = np.sqrt(D * 2 * tau)
```

### Step 5: Assign unknown = value

```python
l1, l2, l3 = [D, D, D]
```

### Step 6: Assign S = single_tensor(...)

```python
S = single_tensor(gtab, evals=np.r_[l1, l2, l3], rng=rng)
```

### Step 7: Assign S_array = np.tile(...)

```python
S_array = np.tile(S, (5, 1))
```

### Step 8: Assign stat_weight = 0.1

```python
stat_weight = 0.1
```

### Step 9: Assign start = time.time(...)

```python
start = time.time()
```

### Step 10: Assign mapf_scale_stat_reg_stat = mapm_scale_stat_reg_stat.fit(...)

```python
mapf_scale_stat_reg_stat = mapm_scale_stat_reg_stat.fit(S_array)
```

### Step 11: Assign time_scale_stat_reg_stat = value

```python
time_scale_stat_reg_stat = time.time() - start
```

### Step 12: Assign start = time.time(...)

```python
start = time.time()
```

### Step 13: Assign mapf_scale_adapt_reg_stat = mapm_scale_adapt_reg_stat.fit(...)

```python
mapf_scale_adapt_reg_stat = mapm_scale_adapt_reg_stat.fit(S_array)
```

### Step 14: Assign time_scale_adapt_reg_stat = value

```python
time_scale_adapt_reg_stat = time.time() - start
```

### Step 15: Call assert_equal()

```python
assert_equal(np.all(mapf_scale_stat_reg_stat.mu == mu), True)
```

### Step 16: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 17: Assign mapm_scale_stat_reg_stat = MapmriModel(...)

```python
mapm_scale_stat_reg_stat = MapmriModel(gtab, radial_order=radial_order, anisotropic_scaling=False, dti_scale_estimation=False, static_diffusivity=D, laplacian_regularization=True, laplacian_weighting=stat_weight)
```

### Step 18: Assign mapm_scale_adapt_reg_stat = MapmriModel(...)

```python
mapm_scale_adapt_reg_stat = MapmriModel(gtab, radial_order=radial_order, anisotropic_scaling=False, dti_scale_estimation=True, laplacian_regularization=True, laplacian_weighting=stat_weight)
```

### Step 19: Call assert_equal()

```python
assert_equal(time_scale_stat_reg_stat < time_scale_adapt_reg_stat, True, f'mapf_scale_stat_reg_stat ({time_scale_stat_reg_stat}s) slower than mapf_scale_adapt_reg_stat ({time_scale_adapt_reg_stat}s). It should be the opposite.')
```

### Step 20: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 21: Call assert_almost_equal()

```python
assert_almost_equal(mapf_scale_stat_reg_stat.fitted_signal(), mapf_scale_adapt_reg_stat.fitted_signal())
```


## Complete Example

```python
# Setup
# Fixtures: radial_order, rng

# Workflow
gtab = get_gtab_taiwan_dsi()
D = 0.0007
tau = 1 / (4 * np.pi ** 2)
mu = np.sqrt(D * 2 * tau)
l1, l2, l3 = [D, D, D]
S = single_tensor(gtab, evals=np.r_[l1, l2, l3], rng=rng)
S_array = np.tile(S, (5, 1))
stat_weight = 0.1
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    mapm_scale_stat_reg_stat = MapmriModel(gtab, radial_order=radial_order, anisotropic_scaling=False, dti_scale_estimation=False, static_diffusivity=D, laplacian_regularization=True, laplacian_weighting=stat_weight)
    mapm_scale_adapt_reg_stat = MapmriModel(gtab, radial_order=radial_order, anisotropic_scaling=False, dti_scale_estimation=True, laplacian_regularization=True, laplacian_weighting=stat_weight)
start = time.time()
mapf_scale_stat_reg_stat = mapm_scale_stat_reg_stat.fit(S_array)
time_scale_stat_reg_stat = time.time() - start
start = time.time()
mapf_scale_adapt_reg_stat = mapm_scale_adapt_reg_stat.fit(S_array)
time_scale_adapt_reg_stat = time.time() - start
assert_equal(np.all(mapf_scale_stat_reg_stat.mu == mu), True)
if not platform.system() == 'Windows':
    assert_equal(time_scale_stat_reg_stat < time_scale_adapt_reg_stat, True, f'mapf_scale_stat_reg_stat ({time_scale_stat_reg_stat}s) slower than mapf_scale_adapt_reg_stat ({time_scale_adapt_reg_stat}s). It should be the opposite.')
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    assert_almost_equal(mapf_scale_stat_reg_stat.fitted_signal(), mapf_scale_adapt_reg_stat.fitted_signal())
```

## Next Steps


---

*Source: test_mapmri.py:374 | Complexity: Advanced | Last updated: 2026-05-18*