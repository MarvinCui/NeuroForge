# How To: Mapmri Isotropic Design Matrix Separability

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mapmri isotropic design matrix separability

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
assert_array_almost_equal(M, M_reconstructed)
```

### Step 2: Assign tau = value

```python
tau = 1 / (4 * np.pi ** 2)
```

### Step 3: Assign qvals = value

```python
qvals = np.sqrt(gtab.bvals / tau) / (2 * np.pi)
```

### Step 4: Assign q = value

```python
q = gtab.bvecs * qvals[:, None]
```

### Step 5: Assign mu = 0.0003

```python
mu = 0.0003
```

### Step 6: Assign M_dependent = mapmri.mapmri_isotropic_M_mu_dependent(...)

```python
M_dependent = mapmri.mapmri_isotropic_M_mu_dependent(radial_order, mu, qvals)
```

### Step 7: Assign M_reconstructed = value

```python
M_reconstructed = M_independent * M_dependent
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(M, M_reconstructed)
```

### Step 9: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 10: Assign M = mapmri.mapmri_isotropic_phi_matrix(...)

```python
M = mapmri.mapmri_isotropic_phi_matrix(radial_order, mu, q)
```

### Step 11: Assign M_independent = mapmri.mapmri_isotropic_M_mu_independent(...)

```python
M_independent = mapmri.mapmri_isotropic_M_mu_independent(radial_order, q)
```


## Complete Example

```python
# Setup
# Fixtures: radial_order

# Workflow
gtab = get_gtab_taiwan_dsi()
tau = 1 / (4 * np.pi ** 2)
qvals = np.sqrt(gtab.bvals / tau) / (2 * np.pi)
q = gtab.bvecs * qvals[:, None]
mu = 0.0003
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    M = mapmri.mapmri_isotropic_phi_matrix(radial_order, mu, q)
    M_independent = mapmri.mapmri_isotropic_M_mu_independent(radial_order, q)
M_dependent = mapmri.mapmri_isotropic_M_mu_dependent(radial_order, mu, qvals)
M_reconstructed = M_independent * M_dependent
assert_array_almost_equal(M, M_reconstructed)
```

## Next Steps


---

*Source: test_mapmri.py:789 | Complexity: Advanced | Last updated: 2026-05-18*