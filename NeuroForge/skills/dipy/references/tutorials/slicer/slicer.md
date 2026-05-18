# How To: Slicer

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test slicer

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `tempfile`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.align.reslice`
- `dipy.align.tests.test_streamlinear`
- `dipy.data`
- `dipy.direction`
- `dipy.reconst.dti`
- `dipy.reconst.shm`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking.stopping_criterion`
- `dipy.tracking.streamline`
- `dipy.tracking.tracker`
- `dipy.utils.optpkg`
- `dipy.viz`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign scene = window.Scene(...)

```python
scene = window.Scene()
```

### Step 2: Assign data = value

```python
data = 255 * rng.random((50, 50, 50))
```

### Step 3: Assign affine = np.diag(...)

```python
affine = np.diag([1, 3, 2, 1])
```

### Step 4: Assign unknown = reslice(...)

```python
data2, affine2 = reslice(data, affine, zooms=(1, 3, 2), new_zooms=(1, 1, 1))
```

### Step 5: Assign slicer = actor.slicer(...)

```python
slicer = actor.slicer(data2, affine=affine2, interpolation='linear')
```

### Step 6: Call slicer.display()

```python
slicer.display(x=None, y=None, z=25)
```

### Step 7: Call scene.add()

```python
scene.add(slicer)
```

### Step 8: Call scene.reset_camera()

```python
scene.reset_camera()
```

### Step 9: Call scene.reset_clipping_range()

```python
scene.reset_clipping_range()
```

### Step 10: Assign arr = window.snapshot(...)

```python
arr = window.snapshot(scene, offscreen=True)
```

### Step 11: Assign report = window.analyze_snapshot(...)

```python
report = window.analyze_snapshot(arr, find_objects=True)
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(report.objects, 1)
```

### Step 13: Call npt.assert_array_equal()

```python
npt.assert_array_equal([1, 3, 2] * np.array(data.shape), np.array(slicer.shape))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
scene = window.Scene()
data = 255 * rng.random((50, 50, 50))
affine = np.diag([1, 3, 2, 1])
data2, affine2 = reslice(data, affine, zooms=(1, 3, 2), new_zooms=(1, 1, 1))
slicer = actor.slicer(data2, affine=affine2, interpolation='linear')
slicer.display(x=None, y=None, z=25)
scene.add(slicer)
scene.reset_camera()
scene.reset_clipping_range()
arr = window.snapshot(scene, offscreen=True)
report = window.analyze_snapshot(arr, find_objects=True)
npt.assert_equal(report.objects, 1)
npt.assert_array_equal([1, 3, 2] * np.array(data.shape), np.array(slicer.shape))
```

## Next Steps


---

*Source: test_fury.py:34 | Complexity: Advanced | Last updated: 2026-05-18*