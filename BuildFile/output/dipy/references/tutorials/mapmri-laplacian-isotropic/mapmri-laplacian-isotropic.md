# How To: Mapmri Laplacian Isotropic

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mapmri laplacian isotropic

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
# Fixtures: radial_order
```

## Step-by-Step Guide

### Step 1: Assign gtab = get_gtab_taiwan_dsi(...)

```python
gtab = get_gtab_taiwan_dsi()
```

**Verification:**
```python
assert_almost_equal(norm_of_laplacian, norm_of_laplacian_gt)
```

### Step 2: Assign unknown = value

```python
l1, l2, l3 = [0.0003, 0.0003, 0.0003]
```

### Step 3: Assign S = single_tensor(...)

```python
S = single_tensor(gtab, evals=np.r_[l1, l2, l3])
```

### Step 4: Assign mapfit = mapm.fit(...)

```python
mapfit = mapm.fit(S)
```

### Step 5: Assign tau = value

```python
tau = 1 / (4 * np.pi ** 2)
```

### Step 6: Assign norm_of_laplacian_gt = value

```python
norm_of_laplacian_gt = (3 * (l1 ** 2 + l2 ** 2 + l3 ** 2) + 2 * l2 * l3 + 2 * l1 * (l2 + l3)) * (np.pi ** (5 / 2.0) * tau) / np.sqrt(2 * l1 * l2 * l3 * tau)
```

### Step 7: Assign laplacian_matrix = mapmri.mapmri_isotropic_laplacian_reg_matrix(...)

```python
laplacian_matrix = mapmri.mapmri_isotropic_laplacian_reg_matrix(radial_order, mapfit.mu[0])
```

### Step 8: Assign coef = value

```python
coef = mapfit._mapmri_coef
```

### Step 9: Assign norm_of_laplacian = np.dot(...)

```python
norm_of_laplacian = np.dot(np.dot(coef, laplacian_matrix), coef)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(norm_of_laplacian, norm_of_laplacian_gt)
```

### Step 11: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 12: Assign mapm = MapmriModel(...)

```python
mapm = MapmriModel(gtab, radial_order=radial_order, laplacian_regularization=False, anisotropic_scaling=False)
```


## Complete Example

```python
# Setup
# Fixtures: radial_order

# Workflow
gtab = get_gtab_taiwan_dsi()
l1, l2, l3 = [0.0003, 0.0003, 0.0003]
S = single_tensor(gtab, evals=np.r_[l1, l2, l3])
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    mapm = MapmriModel(gtab, radial_order=radial_order, laplacian_regularization=False, anisotropic_scaling=False)
mapfit = mapm.fit(S)
tau = 1 / (4 * np.pi ** 2)
norm_of_laplacian_gt = (3 * (l1 ** 2 + l2 ** 2 + l3 ** 2) + 2 * l2 * l3 + 2 * l1 * (l2 + l3)) * (np.pi ** (5 / 2.0) * tau) / np.sqrt(2 * l1 * l2 * l3 * tau)
laplacian_matrix = mapmri.mapmri_isotropic_laplacian_reg_matrix(radial_order, mapfit.mu[0])
coef = mapfit._mapmri_coef
norm_of_laplacian = np.dot(np.dot(coef, laplacian_matrix), coef)
assert_almost_equal(norm_of_laplacian, norm_of_laplacian_gt)
```

## Next Steps


---

*Source: test_mapmri.py:669 | Complexity: Advanced | Last updated: 2026-05-18*