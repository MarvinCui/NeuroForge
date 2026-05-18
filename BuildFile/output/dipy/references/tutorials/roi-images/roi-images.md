# How To: Roi Images

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test roi images

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `tempfile`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.io.stateful_tractogram`
- `dipy.io.utils`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`
- `dipy.utils.optpkg`
- `fury`
- `dipy.viz.horizon.app`
- `dipy.segment.tests.test_bundles`
- `dipy.segment.tests.test_bundles`
- `dipy.viz`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign img1 = rng.random(...)

```python
img1 = rng.random((5, 5, 5))
```

### Step 2: Assign img2 = np.zeros(...)

```python
img2 = np.zeros((5, 5, 5))
```

### Step 3: Assign unknown = 1

```python
img2[2, 2, 2] = 1
```

### Step 4: Assign img3 = np.zeros(...)

```python
img3 = np.zeros((5, 5, 5))
```

### Step 5: Assign unknown = 1

```python
img3[0, :, :] = 1
```

### Step 6: Assign images = value

```python
images = [(img1, np.eye(4)), (img2, np.eye(4), '/test/filename.nii.gz'), (img3, np.eye(4), '/test/filename.nii.gz')]
```

### Step 7: Assign show_m = horizon(...)

```python
show_m = horizon(images=images, return_showm=True)
```

### Step 8: Assign analysis = window.analyze_scene(...)

```python
analysis = window.analyze_scene(show_m.scene)
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(analysis.actors, 0)
```

### Step 10: Assign arr = window.snapshot(...)

```python
arr = window.snapshot(show_m.scene)
```

### Step 11: Assign report = window.analyze_snapshot(...)

```python
report = window.analyze_snapshot(arr, colors=[(0, 0, 0), (255, 255, 255)])
```

### Step 12: Call npt.assert_array_equal()

```python
npt.assert_array_equal(report.colors_found, [True, True])
```

### Step 13: Assign show_m = horizon(...)

```python
show_m = horizon(images=images, roi_images=True, return_showm=True)
```

### Step 14: Assign analysis = window.analyze_scene(...)

```python
analysis = window.analyze_scene(show_m.scene)
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(analysis.actors, 3)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
img1 = rng.random((5, 5, 5))
img2 = np.zeros((5, 5, 5))
img2[2, 2, 2] = 1
img3 = np.zeros((5, 5, 5))
img3[0, :, :] = 1
images = [(img1, np.eye(4)), (img2, np.eye(4), '/test/filename.nii.gz'), (img3, np.eye(4), '/test/filename.nii.gz')]
show_m = horizon(images=images, return_showm=True)
analysis = window.analyze_scene(show_m.scene)
npt.assert_equal(analysis.actors, 0)
arr = window.snapshot(show_m.scene)
report = window.analyze_snapshot(arr, colors=[(0, 0, 0), (255, 255, 255)])
npt.assert_array_equal(report.colors_found, [True, True])
show_m = horizon(images=images, roi_images=True, return_showm=True)
analysis = window.analyze_scene(show_m.scene)
npt.assert_equal(analysis.actors, 3)
```

## Next Steps


---

*Source: test_apps.py:275 | Complexity: Advanced | Last updated: 2026-05-18*