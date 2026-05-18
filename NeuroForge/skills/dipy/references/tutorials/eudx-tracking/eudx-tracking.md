# How To: Eudx Tracking

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the eudx_tracking function with PeaksAndMetrics.

## Prerequisites

**Required Modules:**
- `warnings`
- `nibabel`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst.shm`
- `dipy.tracking`
- `dipy.tracking.stopping_criterion`
- `dipy.tracking.streamline`
- `dipy.tracking.utils`


## Step-by-Step Guide

### Step 1: 'Test the eudx_tracking function with PeaksAndMetrics.'

```python
'Test the eudx_tracking function with PeaksAndMetrics.'
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

### Step 7: Assign pam = PeaksAndMetrics(...)

```python
pam = PeaksAndMetrics()
```

### Step 8: Assign pam.sphere = sphere

```python
pam.sphere = sphere
```

### Step 9: Assign pam.peak_values = value

```python
pam.peak_values = peaks_values_lookup[simple_image]
```

### Step 10: Assign pam.peak_indices = value

```python
pam.peak_indices = peaks_indices_lookup[simple_image]
```

### Step 11: Assign pam.odf_vertices = value

```python
pam.odf_vertices = sphere.vertices
```

### Step 12: Assign pam.ang_thr = 90

```python
pam.ang_thr = 90
```

### Step 13: Assign mask = unknown.astype(...)

```python
mask = (simple_image >= 0).astype(float)
```

### Step 14: Assign sc = ThresholdStoppingCriterion(...)

```python
sc = ThresholdStoppingCriterion(mask, 0.5)
```

### Step 15: Assign seeds = np.array(...)

```python
seeds = np.array([[1.0, 1.0, 1.0], [2.0, 4.0, 1.0], [1.0, 3.0, 1.0]])
```

### Step 16: Assign streamlines = list(...)

```python
streamlines = list(tracker.eudx_tracking(seeds, sc, np.eye(4), pam=pam, sphere=sphere, step_size=1.0, max_angle=90, pmf_threshold=0.01, min_len=0, return_all=True))
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(len(streamlines), len(seeds))
```

### Step 18: Assign streamlines_explicit = list(...)

```python
streamlines_explicit = list(tracker.eudx_tracking(seeds, sc, np.eye(4), pam=pam, sphere=sphere, step_size=1.0, max_angle=90, pmf_threshold=0.01, min_len=0, return_all=True, nbr_threads=2))
```

### Step 19: Call npt.assert_equal()

```python
npt.assert_equal(len(streamlines_explicit), len(seeds))
```


## Complete Example

```python
# Workflow
'Test the eudx_tracking function with PeaksAndMetrics.'
sphere = HemiSphere.from_sphere(unit_octahedron)
peaks_values_lookup = np.array([[0.0, 0.0], [1.0, 0.0], [1.0, 0.0], [0.5, 0.5]])
peaks_indices_lookup = np.array([[-1, -1], [0, -1], [1, -1], [0, 1]])
simple_image = np.zeros([5, 6, 3], dtype=int)
simple_image[:, :, 1] = np.array([[0, 1, 0, 1, 0, 0], [0, 1, 0, 1, 0, 0], [0, 3, 2, 2, 2, 0], [0, 1, 0, 0, 0, 0], [0, 1, 0, 0, 0, 0]])
pam = PeaksAndMetrics()
pam.sphere = sphere
pam.peak_values = peaks_values_lookup[simple_image]
pam.peak_indices = peaks_indices_lookup[simple_image]
pam.odf_vertices = sphere.vertices
pam.ang_thr = 90
mask = (simple_image >= 0).astype(float)
sc = ThresholdStoppingCriterion(mask, 0.5)
seeds = np.array([[1.0, 1.0, 1.0], [2.0, 4.0, 1.0], [1.0, 3.0, 1.0]])
streamlines = list(tracker.eudx_tracking(seeds, sc, np.eye(4), pam=pam, sphere=sphere, step_size=1.0, max_angle=90, pmf_threshold=0.01, min_len=0, return_all=True))
npt.assert_equal(len(streamlines), len(seeds))
streamlines_explicit = list(tracker.eudx_tracking(seeds, sc, np.eye(4), pam=pam, sphere=sphere, step_size=1.0, max_angle=90, pmf_threshold=0.01, min_len=0, return_all=True, nbr_threads=2))
npt.assert_equal(len(streamlines_explicit), len(seeds))
```

## Next Steps


---

*Source: test_tracker.py:170 | Complexity: Advanced | Last updated: 2026-05-18*