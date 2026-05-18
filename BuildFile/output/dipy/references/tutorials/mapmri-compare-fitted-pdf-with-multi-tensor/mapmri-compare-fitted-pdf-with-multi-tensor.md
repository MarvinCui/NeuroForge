# How To: Mapmri Compare Fitted Pdf With Multi Tensor

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mapmri compare fitted pdf with multi tensor

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
assert_almost_equal(nmse_pdf, 0.0, 2)
```

### Step 2: Assign unknown = value

```python
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
```

### Step 3: Assign unknown = generate_signal_crossing(...)

```python
S, _ = generate_signal_crossing(gtab, l1, l2, l3)
```

### Step 4: Assign radius_max = 0.02

```python
radius_max = 0.02
```

### Step 5: Assign gridsize = 10

```python
gridsize = 10
```

### Step 6: Assign r_points = mapmri.create_rspace(...)

```python
r_points = mapmri.create_rspace(gridsize, radius_max)
```

### Step 7: Assign mapm = MapmriModel(...)

```python
mapm = MapmriModel(gtab, radial_order=radial_order, laplacian_weighting=0.0001)
```

### Step 8: Assign mapfit = mapm.fit(...)

```python
mapfit = mapm.fit(S)
```

### Step 9: Assign mevals = np.array(...)

```python
mevals = np.array(([l1, l2, l3], [l1, l2, l3]))
```

### Step 10: Assign angl = value

```python
angl = [(0, 0), (60, 0)]
```

### Step 11: Assign pdf_mt = multi_tensor_pdf(...)

```python
pdf_mt = multi_tensor_pdf(r_points, mevals=mevals, angles=angl, fractions=[50, 50])
```

### Step 12: Assign pdf_map = mapfit.pdf(...)

```python
pdf_map = mapfit.pdf(r_points)
```

### Step 13: Assign nmse_pdf = value

```python
nmse_pdf = np.sqrt(np.sum((pdf_mt - pdf_map) ** 2)) / pdf_mt.sum()
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(nmse_pdf, 0.0, 2)
```


## Complete Example

```python
# Setup
# Fixtures: radial_order

# Workflow
gtab = get_gtab_taiwan_dsi()
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
S, _ = generate_signal_crossing(gtab, l1, l2, l3)
radius_max = 0.02
gridsize = 10
r_points = mapmri.create_rspace(gridsize, radius_max)
mapm = MapmriModel(gtab, radial_order=radial_order, laplacian_weighting=0.0001)
mapfit = mapm.fit(S)
mevals = np.array(([l1, l2, l3], [l1, l2, l3]))
angl = [(0, 0), (60, 0)]
pdf_mt = multi_tensor_pdf(r_points, mevals=mevals, angles=angl, fractions=[50, 50])
pdf_map = mapfit.pdf(r_points)
nmse_pdf = np.sqrt(np.sum((pdf_mt - pdf_map) ** 2)) / pdf_mt.sum()
assert_almost_equal(nmse_pdf, 0.0, 2)
```

## Next Steps


---

*Source: test_mapmri.py:527 | Complexity: Advanced | Last updated: 2026-05-18*