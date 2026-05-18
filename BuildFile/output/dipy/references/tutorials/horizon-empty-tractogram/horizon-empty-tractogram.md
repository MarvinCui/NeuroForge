# How To: Horizon Empty Tractogram

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that empty tractograms are handled gracefully without errors.

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

### Step 1: 'Test that empty tractograms are handled gracefully without errors.'

```python
'Test that empty tractograms are handled gracefully without errors.'
```

### Step 2: Assign empty_streamlines = Streamlines(...)

```python
empty_streamlines = Streamlines()
```

### Step 3: Call empty_streamlines.shrink_data()

```python
empty_streamlines.shrink_data()
```

### Step 4: Assign affine = np.array(...)

```python
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
```

### Step 5: Assign data = value

```python
data = 255 * rng.random((197, 233, 189))
```

### Step 6: Assign vox_size = value

```python
vox_size = (1.0, 1.0, 1.0)
```

### Step 7: Assign header = create_nifti_header(...)

```python
header = create_nifti_header(affine, data.shape, vox_size)
```

### Step 8: Assign sft = StatefulTractogram(...)

```python
sft = StatefulTractogram(empty_streamlines, header, Space.RASMM)
```

### Step 9: Assign tractograms = value

```python
tractograms = [sft]
```

### Step 10: Assign images = value

```python
images = [(data, affine, '/test/filename.nii.gz')]
```

### Step 11: Call warnings.simplefilter()

```python
warnings.simplefilter('always')
```

### Step 12: Call check_for_warnings()

```python
check_for_warnings(w, 'Tractogram 0 is empty and will be skipped.')
```

### Step 13: Call horizon()

```python
horizon(tractograms=tractograms, images=images, cluster=False, world_coords=True, interactive=False, out_png=Path(out_dir) / 'empty-tractogram.png')
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test that empty tractograms are handled gracefully without errors.'
empty_streamlines = Streamlines()
empty_streamlines.shrink_data()
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
data = 255 * rng.random((197, 233, 189))
vox_size = (1.0, 1.0, 1.0)
header = create_nifti_header(affine, data.shape, vox_size)
sft = StatefulTractogram(empty_streamlines, header, Space.RASMM)
tractograms = [sft]
images = [(data, affine, '/test/filename.nii.gz')]
with warnings.catch_warnings(record=True) as w:
    warnings.simplefilter('always')
    with TemporaryDirectory() as out_dir:
        horizon(tractograms=tractograms, images=images, cluster=False, world_coords=True, interactive=False, out_png=Path(out_dir) / 'empty-tractogram.png')
    check_for_warnings(w, 'Tractogram 0 is empty and will be skipped.')
```

## Next Steps


---

*Source: test_apps.py:232 | Complexity: Advanced | Last updated: 2026-05-18*