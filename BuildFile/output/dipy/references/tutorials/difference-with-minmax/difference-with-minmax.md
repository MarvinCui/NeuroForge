# How To: Difference With Minmax

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test difference with minmax

## Prerequisites

**Required Modules:**
- `io`
- `pickle`
- `random`
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.direction.pmf`
- `dipy.io.gradients`
- `dipy.reconst.odf`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking.utils`


## Step-by-Step Guide

### Step 1: Assign mevals = np.array(...)

```python
mevals = np.array([[0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003], [0.0015, 5e-05, 5e-05], [0.0015, 0.0015, 0.0015]])
```

**Verification:**
```python
assert_equal(len(values_1), 3)
```

### Step 2: Assign angles = value

```python
angles = [(0, 0), (45, 0), (90, 0), (90, 90), (0, 0)]
```

**Verification:**
```python
assert_equal(len(values_2), 3)
```

### Step 3: Assign fractions = value

```python
fractions = [20, 20, 10, 1, 100 - 20 - 20 - 10 - 1]
```

**Verification:**
```python
assert_equal(len(values_3), 4)
```

### Step 4: Assign unknown = _create_mt_sim(...)

```python
odf_gt, sticks, sphere = _create_mt_sim(mevals, angles, fractions, 100, None)
```

**Verification:**
```python
assert_equal(len(values_4), 3)
```

### Step 5: Assign odf_gt_minmax = value

```python
odf_gt_minmax = (odf_gt - odf_gt.min()) / (odf_gt.max() - odf_gt.min())
```

**Verification:**
```python
assert_almost_equal(values_1, values_4)
```

### Step 6: Assign unknown = peak_directions(...)

```python
_, values_1, _ = peak_directions(odf_gt, sphere, relative_peak_threshold=0.3, min_separation_angle=25.0)
```

### Step 7: Call assert_equal()

```python
assert_equal(len(values_1), 3)
```

### Step 8: Assign unknown = peak_directions(...)

```python
_, values_2, _ = peak_directions(odf_gt_minmax, sphere, relative_peak_threshold=0.3, min_separation_angle=25.0)
```

### Step 9: Call assert_equal()

```python
assert_equal(len(values_2), 3)
```

### Step 10: Assign unknown = 0.0

```python
odf_gt[odf_gt.argmin()] = 0.0
```

### Step 11: Assign unknown = peak_directions(...)

```python
_, values_3, _ = peak_directions(odf_gt, sphere, relative_peak_threshold=0.3, min_separation_angle=25.0)
```

### Step 12: Call assert_equal()

```python
assert_equal(len(values_3), 4)
```

### Step 13: Assign unknown = peak_directions(...)

```python
directions, values_4, indices = peak_directions(odf_gt, sphere, relative_peak_threshold=0.6, min_separation_angle=25.0)
```

### Step 14: Call assert_equal()

```python
assert_equal(len(values_4), 3)
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(values_1, values_4)
```


## Complete Example

```python
# Workflow
mevals = np.array([[0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003], [0.0015, 5e-05, 5e-05], [0.0015, 0.0015, 0.0015]])
angles = [(0, 0), (45, 0), (90, 0), (90, 90), (0, 0)]
fractions = [20, 20, 10, 1, 100 - 20 - 20 - 10 - 1]
odf_gt, sticks, sphere = _create_mt_sim(mevals, angles, fractions, 100, None)
odf_gt_minmax = (odf_gt - odf_gt.min()) / (odf_gt.max() - odf_gt.min())
_, values_1, _ = peak_directions(odf_gt, sphere, relative_peak_threshold=0.3, min_separation_angle=25.0)
assert_equal(len(values_1), 3)
_, values_2, _ = peak_directions(odf_gt_minmax, sphere, relative_peak_threshold=0.3, min_separation_angle=25.0)
assert_equal(len(values_2), 3)
odf_gt[odf_gt.argmin()] = 0.0
_, values_3, _ = peak_directions(odf_gt, sphere, relative_peak_threshold=0.3, min_separation_angle=25.0)
assert_equal(len(values_3), 4)
directions, values_4, indices = peak_directions(odf_gt, sphere, relative_peak_threshold=0.6, min_separation_angle=25.0)
assert_equal(len(values_4), 3)
assert_almost_equal(values_1, values_4)
```

## Next Steps


---

*Source: test_peaks.py:398 | Complexity: Advanced | Last updated: 2026-05-18*