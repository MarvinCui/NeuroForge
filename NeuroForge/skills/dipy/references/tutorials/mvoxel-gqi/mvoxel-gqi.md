# How To: Mvoxel Gqi

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mvoxel gqi

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst.gqi`
- `dipy.reconst.odf`
- `dipy.reconst.tests.test_dsi`
- `dipy.sims.voxel`


## Step-by-Step Guide

### Step 1: Assign unknown = dsi_voxels(...)

```python
data, gtab = dsi_voxels()
```

**Verification:**
```python
assert_equal(directions.shape[0], 2)
```

### Step 2: Assign sphere = get_sphere(...)

```python
sphere = get_sphere(name='symmetric724')
```

**Verification:**
```python
assert_equal(directions.shape[0], 2)
```

### Step 3: Assign gq = GeneralizedQSamplingModel(...)

```python
gq = GeneralizedQSamplingModel(gtab, method='standard')
```

### Step 4: Assign gqfit = gq.fit(...)

```python
gqfit = gq.fit(data)
```

### Step 5: Assign all_odfs = gqfit.odf(...)

```python
all_odfs = gqfit.odf(sphere)
```

### Step 6: Assign odf = value

```python
odf = all_odfs[0, 0, 0]
```

### Step 7: Assign unknown = peak_directions(...)

```python
directions, values, indices = peak_directions(odf, sphere, relative_peak_threshold=0.35, min_separation_angle=25)
```

### Step 8: Call assert_equal()

```python
assert_equal(directions.shape[0], 2)
```

### Step 9: Assign odf = value

```python
odf = all_odfs[-1, -1, -1]
```

### Step 10: Assign unknown = peak_directions(...)

```python
directions, values, indices = peak_directions(odf, sphere, relative_peak_threshold=0.35, min_separation_angle=25)
```

### Step 11: Call assert_equal()

```python
assert_equal(directions.shape[0], 2)
```


## Complete Example

```python
# Workflow
data, gtab = dsi_voxels()
sphere = get_sphere(name='symmetric724')
gq = GeneralizedQSamplingModel(gtab, method='standard')
gqfit = gq.fit(data)
all_odfs = gqfit.odf(sphere)
odf = all_odfs[0, 0, 0]
directions, values, indices = peak_directions(odf, sphere, relative_peak_threshold=0.35, min_separation_angle=25)
assert_equal(directions.shape[0], 2)
odf = all_odfs[-1, -1, -1]
directions, values, indices = peak_directions(odf, sphere, relative_peak_threshold=0.35, min_separation_angle=25)
assert_equal(directions.shape[0], 2)
```

## Next Steps


---

*Source: test_gqi.py:60 | Complexity: Advanced | Last updated: 2026-05-18*