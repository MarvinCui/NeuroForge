# How To: Mapmri Metrics Anisotropic

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mapmri metrics anisotropic

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
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
```

**Verification:**
```python
assert_almost_equal(mapfit.rtpp(), rtpp_gt, 5)
```

### Step 3: Assign unknown = generate_signal_crossing(...)

```python
S, _ = generate_signal_crossing(gtab, l1, l2, l3, angle2=0)
```

**Verification:**
```python
assert_almost_equal(mapfit.rtop(), rtop_gt, 5)
```

### Step 4: Assign mapm = MapmriModel(...)

```python
mapm = MapmriModel(gtab, radial_order=radial_order, laplacian_regularization=False)
```

**Verification:**
```python
assert_equal(len(w), 3)
```

### Step 5: Assign mapfit = mapm.fit(...)

```python
mapfit = mapm.fit(S)
```

**Verification:**
```python
assert_(issubclass(l_w.category, UserWarning))
```

### Step 6: Assign tau = value

```python
tau = 1 / (4 * np.pi ** 2)
```

**Verification:**
```python
assert_('model bval_threshold must be lower than 2000'.lower() in str(l_w.message).lower())
```

### Step 7: Assign rtpp_gt = value

```python
rtpp_gt = 1.0 / (2 * np.sqrt(np.pi * l1 * tau))
```

**Verification:**
```python
assert_almost_equal(ng, 0.0, 5)
```

### Step 8: Assign rtap_gt = value

```python
rtap_gt = 1.0 / (2 * np.sqrt(np.pi * l2 * tau)) * 1.0 / (2 * np.sqrt(np.pi * l3 * tau))
```

**Verification:**
```python
assert_almost_equal(ng_parallel, 0.0, 5)
```

### Step 9: Assign rtop_gt = value

```python
rtop_gt = rtpp_gt * rtap_gt
```

**Verification:**
```python
assert_almost_equal(ng_perpendicular, 0.0, 5)
```

### Step 10: Assign msd_gt = value

```python
msd_gt = 2 * (l1 + l2 + l3) * tau
```

**Verification:**
```python
assert_almost_equal(mapfit.msd(), msd_gt, 5)
```

### Step 11: Assign qiv_gt = value

```python
qiv_gt = 64 * np.pi ** (7 / 2.0) * (l1 * l2 * l3 * tau ** 3) ** (3 / 2.0) / ((l2 * l3 + l1 * (l2 + l3)) * tau ** 2)
```

**Verification:**
```python
assert_almost_equal(mapfit.qiv(), qiv_gt, 5)
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(mapfit.rtap(), rtap_gt, 5)
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(mapfit.rtpp(), rtpp_gt, 5)
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(mapfit.rtop(), rtop_gt, 5)
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(ng, 0.0, 5)
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(ng_parallel, 0.0, 5)
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(ng_perpendicular, 0.0, 5)
```

### Step 18: Call assert_almost_equal()

```python
assert_almost_equal(mapfit.msd(), msd_gt, 5)
```

### Step 19: Call assert_almost_equal()

```python
assert_almost_equal(mapfit.qiv(), qiv_gt, 5)
```

### Step 20: Assign ng = mapfit.ng(...)

```python
ng = mapfit.ng()
```

### Step 21: Assign ng_parallel = mapfit.ng_parallel(...)

```python
ng_parallel = mapfit.ng_parallel()
```

### Step 22: Assign ng_perpendicular = mapfit.ng_perpendicular(...)

```python
ng_perpendicular = mapfit.ng_perpendicular()
```

### Step 23: Call assert_equal()

```python
assert_equal(len(w), 3)
```

### Step 24: Call assert_()

```python
assert_(issubclass(l_w.category, UserWarning))
```

### Step 25: Call assert_()

```python
assert_('model bval_threshold must be lower than 2000'.lower() in str(l_w.message).lower())
```


## Complete Example

```python
# Setup
# Fixtures: radial_order

# Workflow
gtab = get_gtab_taiwan_dsi()
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
S, _ = generate_signal_crossing(gtab, l1, l2, l3, angle2=0)
mapm = MapmriModel(gtab, radial_order=radial_order, laplacian_regularization=False)
mapfit = mapm.fit(S)
tau = 1 / (4 * np.pi ** 2)
rtpp_gt = 1.0 / (2 * np.sqrt(np.pi * l1 * tau))
rtap_gt = 1.0 / (2 * np.sqrt(np.pi * l2 * tau)) * 1.0 / (2 * np.sqrt(np.pi * l3 * tau))
rtop_gt = rtpp_gt * rtap_gt
msd_gt = 2 * (l1 + l2 + l3) * tau
qiv_gt = 64 * np.pi ** (7 / 2.0) * (l1 * l2 * l3 * tau ** 3) ** (3 / 2.0) / ((l2 * l3 + l1 * (l2 + l3)) * tau ** 2)
assert_almost_equal(mapfit.rtap(), rtap_gt, 5)
assert_almost_equal(mapfit.rtpp(), rtpp_gt, 5)
assert_almost_equal(mapfit.rtop(), rtop_gt, 5)
with warnings.catch_warnings(record=True) as w:
    ng = mapfit.ng()
    ng_parallel = mapfit.ng_parallel()
    ng_perpendicular = mapfit.ng_perpendicular()
    assert_equal(len(w), 3)
    for l_w in w:
        assert_(issubclass(l_w.category, UserWarning))
        assert_('model bval_threshold must be lower than 2000'.lower() in str(l_w.message).lower())
assert_almost_equal(ng, 0.0, 5)
assert_almost_equal(ng_parallel, 0.0, 5)
assert_almost_equal(ng_perpendicular, 0.0, 5)
assert_almost_equal(mapfit.msd(), msd_gt, 5)
assert_almost_equal(mapfit.qiv(), qiv_gt, 5)
```

## Next Steps


---

*Source: test_mapmri.py:551 | Complexity: Advanced | Last updated: 2026-05-18*