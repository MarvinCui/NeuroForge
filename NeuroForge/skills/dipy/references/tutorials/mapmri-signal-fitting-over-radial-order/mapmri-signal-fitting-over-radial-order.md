# How To: Mapmri Signal Fitting Over Radial Order

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mapmri signal fitting over radial order

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
# Fixtures: order_max
```

## Step-by-Step Guide

### Step 1: Assign gtab = get_gtab_taiwan_dsi(...)

```python
gtab = get_gtab_taiwan_dsi()
```

**Verification:**
```python
assert_equal(np.diff(error_array) < 0.0, True)
```

### Step 2: Assign unknown = value

```python
l1, l2, l3 = [0.0012, 0.0003, 0.0003]
```

### Step 3: Assign unknown = generate_signal_crossing(...)

```python
S, _ = generate_signal_crossing(gtab, l1, l2, l3, angle2=60)
```

### Step 4: Assign orders = value

```python
orders = [0, 4, 8]
```

### Step 5: Assign error_array = np.zeros(...)

```python
error_array = np.zeros(len(orders))
```

### Step 6: Call assert_equal()

```python
assert_equal(np.diff(error_array) < 0.0, True)
```

### Step 7: Assign mapm = MapmriModel(...)

```python
mapm = MapmriModel(gtab, radial_order=order, laplacian_regularization=False)
```

### Step 8: Assign mapfit = mapm.fit(...)

```python
mapfit = mapm.fit(S)
```

### Step 9: Assign S_reconst = mapfit.predict(...)

```python
S_reconst = mapfit.predict(gtab, S0=100.0)
```

### Step 10: Assign unknown = np.mean(...)

```python
error_array[i] = np.mean((S - S_reconst) ** 2)
```


## Complete Example

```python
# Setup
# Fixtures: order_max

# Workflow
gtab = get_gtab_taiwan_dsi()
l1, l2, l3 = [0.0012, 0.0003, 0.0003]
S, _ = generate_signal_crossing(gtab, l1, l2, l3, angle2=60)
orders = [0, 4, 8]
error_array = np.zeros(len(orders))
for i, order in enumerate(orders):
    mapm = MapmriModel(gtab, radial_order=order, laplacian_regularization=False)
    mapfit = mapm.fit(S)
    S_reconst = mapfit.predict(gtab, S0=100.0)
    error_array[i] = np.mean((S - S_reconst) ** 2)
assert_equal(np.diff(error_array) < 0.0, True)
```

## Next Steps


---

*Source: test_mapmri.py:443 | Complexity: Advanced | Last updated: 2026-05-18*