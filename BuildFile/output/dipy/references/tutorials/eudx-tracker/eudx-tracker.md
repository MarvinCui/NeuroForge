# How To: Eudx Tracker

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: This tests that the Peaks And Metrics Direction Getter plays nice
LocalTracking and produces reasonable streamlines in a simple example.

## Prerequisites

**Required Modules:**
- `warnings`
- `nibabel`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction`
- `dipy.reconst.csdeconv`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking.local_tracking`
- `dipy.tracking.stopping_criterion`
- `dipy.tracking.streamline`
- `dipy.tracking.utils`


## Step-by-Step Guide

### Step 1: 'This tests that the Peaks And Metrics Direction Getter plays nice\n    LocalTracking and produces reasonable streamlines in a simple example.\n    '

```python
'This tests that the Peaks And Metrics Direction Getter plays nice\n    LocalTracking and produces reasonable streamlines in a simple example.\n    '
```

### Step 2: Assign sphere = HemiSphere.from_sphere(...)

```python
sphere = HemiSphere.from_sphere(unit_octahedron)
```

### Step 3: Assign peaks_values_lookup = np.array(...)

```python
peaks_values_lookup = np.array([[0.0, 0.0], [1.0, 0.0], [1.0, 0.0], [0.5, 0.5]])
```

### Step 4: Assign peaks_indices_lookup = np.array(...)

```python
peaks_indices_lookup = np.array([[-1, -1], [0, -1], [1, -1], [0, 1]])
```

### Step 5: Assign simple_image = np.zeros(...)

```python
simple_image = np.zeros([5, 6, 3], dtype=int)
```

### Step 6: Assign unknown = np.array(...)

```python
simple_image[:, :, 1] = np.array([[0, 1, 0, 1, 0, 0], [0, 1, 0, 1, 0, 0], [0, 3, 2, 2, 2, 0], [0, 1, 0, 0, 0, 0], [0, 1, 0, 0, 0, 0]])
```

### Step 7: Assign dg = PeaksAndMetrics(...)

```python
dg = PeaksAndMetrics()
```

### Step 8: Assign dg.sphere = sphere

```python
dg.sphere = sphere
```

### Step 9: Assign dg.peak_values = value

```python
dg.peak_values = peaks_values_lookup[simple_image]
```

### Step 10: Assign dg.peak_indices = value

```python
dg.peak_indices = peaks_indices_lookup[simple_image]
```

### Step 11: Assign dg.ang_thr = 90

```python
dg.ang_thr = 90
```

### Step 12: Assign mask = unknown.astype(...)

```python
mask = (simple_image >= 0).astype(float)
```

### Step 13: Assign sc = ThresholdStoppingCriterion(...)

```python
sc = ThresholdStoppingCriterion(mask, 0.5)
```

### Step 14: Assign seeds = value

```python
seeds = [np.array([1.0, 1.0, 1.0]), np.array([2.0, 4.0, 1.0]), np.array([1.0, 3.0, 1.0]), np.array([4.0, 4.0, 1.0])]
```

### Step 15: Assign streamlines = assert_warns(...)

```python
streamlines = assert_warns(DeprecationWarning, LocalTracking, dg, sc, seeds, np.eye(4), 1.0)
```

### Step 16: Assign expected = value

```python
expected = [np.array([[0.0, 1.0, 1.0], [1.0, 1.0, 1.0], [2.0, 1.0, 1.0], [3.0, 1.0, 1.0], [4.0, 1.0, 1.0]]), np.array([[2.0, 0.0, 1.0], [2.0, 1.0, 1.0], [2.0, 2.0, 1.0], [2.0, 3.0, 1.0], [2.0, 4.0, 1.0], [2.0, 5.0, 1.0]]), np.array([[0.0, 3.0, 1.0], [1.0, 3.0, 1.0], [2.0, 3.0, 1.0], [2.0, 4.0, 1.0], [2.0, 5.0, 1.0]]), np.array([[4.0, 4.0, 1.0]])]
```

### Step 17: Call npt.assert_()

```python
npt.assert_(np.allclose(sl, expected[i]))
```


## Complete Example

```python
# Workflow
'This tests that the Peaks And Metrics Direction Getter plays nice\n    LocalTracking and produces reasonable streamlines in a simple example.\n    '
sphere = HemiSphere.from_sphere(unit_octahedron)
peaks_values_lookup = np.array([[0.0, 0.0], [1.0, 0.0], [1.0, 0.0], [0.5, 0.5]])
peaks_indices_lookup = np.array([[-1, -1], [0, -1], [1, -1], [0, 1]])
simple_image = np.zeros([5, 6, 3], dtype=int)
simple_image[:, :, 1] = np.array([[0, 1, 0, 1, 0, 0], [0, 1, 0, 1, 0, 0], [0, 3, 2, 2, 2, 0], [0, 1, 0, 0, 0, 0], [0, 1, 0, 0, 0, 0]])
dg = PeaksAndMetrics()
dg.sphere = sphere
dg.peak_values = peaks_values_lookup[simple_image]
dg.peak_indices = peaks_indices_lookup[simple_image]
dg.ang_thr = 90
mask = (simple_image >= 0).astype(float)
sc = ThresholdStoppingCriterion(mask, 0.5)
seeds = [np.array([1.0, 1.0, 1.0]), np.array([2.0, 4.0, 1.0]), np.array([1.0, 3.0, 1.0]), np.array([4.0, 4.0, 1.0])]
streamlines = assert_warns(DeprecationWarning, LocalTracking, dg, sc, seeds, np.eye(4), 1.0)
expected = [np.array([[0.0, 1.0, 1.0], [1.0, 1.0, 1.0], [2.0, 1.0, 1.0], [3.0, 1.0, 1.0], [4.0, 1.0, 1.0]]), np.array([[2.0, 0.0, 1.0], [2.0, 1.0, 1.0], [2.0, 2.0, 1.0], [2.0, 3.0, 1.0], [2.0, 4.0, 1.0], [2.0, 5.0, 1.0]]), np.array([[0.0, 3.0, 1.0], [1.0, 3.0, 1.0], [2.0, 3.0, 1.0], [2.0, 4.0, 1.0], [2.0, 5.0, 1.0]]), np.array([[4.0, 4.0, 1.0]])]
for i, sl in enumerate(streamlines):
    npt.assert_(np.allclose(sl, expected[i]))
```

## Next Steps


---

*Source: test_tracking.py:977 | Complexity: Advanced | Last updated: 2026-05-18*