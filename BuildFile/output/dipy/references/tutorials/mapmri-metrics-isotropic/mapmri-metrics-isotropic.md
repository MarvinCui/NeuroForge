# How To: Mapmri Metrics Isotropic

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mapmri metrics isotropic

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
assert_almost_equal(mapfit.rtap(), rtap_gt, 5)
```

### Step 2: Assign unknown = value

```python
l1, l2, l3 = [0.0003, 0.0003, 0.0003]
```

**Verification:**
```python
assert_almost_equal(mapfit.rtpp(), rtpp_gt, 5)
```

### Step 3: Assign S = single_tensor(...)

```python
S = single_tensor(gtab, evals=np.r_[l1, l2, l3])
```

**Verification:**
```python
assert_almost_equal(mapfit.rtop(), rtop_gt, 4)
```

### Step 4: Assign mapfit = mapm.fit(...)

```python
mapfit = mapm.fit(S)
```

**Verification:**
```python
assert_almost_equal(mapfit.msd(), msd_gt, 5)
```

### Step 5: Assign tau = value

```python
tau = 1 / (4 * np.pi ** 2)
```

**Verification:**
```python
assert_almost_equal(mapfit.qiv(), qiv_gt, 5)
```

### Step 6: Assign rtpp_gt = value

```python
rtpp_gt = 1.0 / (2 * np.sqrt(np.pi * l1 * tau))
```

### Step 7: Assign rtap_gt = value

```python
rtap_gt = 1.0 / (2 * np.sqrt(np.pi * l2 * tau)) * 1.0 / (2 * np.sqrt(np.pi * l3 * tau))
```

### Step 8: Assign rtop_gt = value

```python
rtop_gt = rtpp_gt * rtap_gt
```

### Step 9: Assign msd_gt = value

```python
msd_gt = 2 * (l1 + l2 + l3) * tau
```

### Step 10: Assign qiv_gt = value

```python
qiv_gt = 64 * np.pi ** (7 / 2.0) * (l1 * l2 * l3 * tau ** 3) ** (3 / 2.0) / ((l2 * l3 + l1 * (l2 + l3)) * tau ** 2)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(mapfit.rtop(), rtop_gt, 4)
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(mapfit.msd(), msd_gt, 5)
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(mapfit.qiv(), qiv_gt, 5)
```

### Step 14: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 15: Assign mapm = MapmriModel(...)

```python
mapm = MapmriModel(gtab, radial_order=radial_order, laplacian_regularization=False, anisotropic_scaling=False)
```

### Step 16: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(mapfit.rtap(), rtap_gt, 5)
```

### Step 18: Call assert_almost_equal()

```python
assert_almost_equal(mapfit.rtpp(), rtpp_gt, 5)
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
rtpp_gt = 1.0 / (2 * np.sqrt(np.pi * l1 * tau))
rtap_gt = 1.0 / (2 * np.sqrt(np.pi * l2 * tau)) * 1.0 / (2 * np.sqrt(np.pi * l3 * tau))
rtop_gt = rtpp_gt * rtap_gt
msd_gt = 2 * (l1 + l2 + l3) * tau
qiv_gt = 64 * np.pi ** (7 / 2.0) * (l1 * l2 * l3 * tau ** 3) ** (3 / 2.0) / ((l2 * l3 + l1 * (l2 + l3)) * tau ** 2)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    assert_almost_equal(mapfit.rtap(), rtap_gt, 5)
    assert_almost_equal(mapfit.rtpp(), rtpp_gt, 5)
assert_almost_equal(mapfit.rtop(), rtop_gt, 4)
assert_almost_equal(mapfit.msd(), msd_gt, 5)
assert_almost_equal(mapfit.qiv(), qiv_gt, 5)
```

## Next Steps


---

*Source: test_mapmri.py:595 | Complexity: Advanced | Last updated: 2026-05-18*