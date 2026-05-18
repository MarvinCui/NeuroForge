# How To: View Round Trip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test get_view / set_view round-trip.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `platform`
- `contextlib`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `matplotlib`
- `matplotlib.lines`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space`
- `mne.utils`
- `mne.viz`
- `mne.viz._brain`
- `mne.viz._brain.colormap`
- `mne.viz.utils`
- `mne.viz._brain`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: renderer_interactive_pyvistaqt, tmp_path, brain_gc, align
```

## Step-by-Step Guide

### Step 1: 'Test get_view / set_view round-trip.'

```python
'Test get_view / set_view round-trip.'
```

**Verification:**
```python
assert_allclose(img, img_1)
```

### Step 2: Assign brain = _create_testing_brain(...)

```python
brain = _create_testing_brain(hemi='lh')
```

### Step 3: Assign img = brain.screenshot(...)

```python
img = brain.screenshot()
```

### Step 4: Assign unknown = brain.get_view(...)

```python
roll, distance, azimuth, elevation, focalpoint = brain.get_view(align=align)
```

### Step 5: Call brain.show_view()

```python
brain.show_view(azimuth=azimuth, elevation=elevation, focalpoint=focalpoint, roll=roll, distance=distance, align=align)
```

### Step 6: Assign img_1 = brain.screenshot(...)

```python
img_1 = brain.screenshot()
```

### Step 7: Call assert_allclose()

```python
assert_allclose(img, img_1)
```

### Step 8: Call _assert_view_allclose()

```python
_assert_view_allclose(brain, roll, distance, azimuth, elevation, focalpoint, align)
```

### Step 9: Assign unknown = value

```python
roll, distance, focalpoint = (1, 500, (1e-05, 1e-05, 1e-05))
```

### Step 10: Assign view_args = dict(...)

```python
view_args = dict(roll=roll, distance=distance, focalpoint=focalpoint, align=align)
```

### Step 11: Call brain.show_view()

```python
brain.show_view(**view_args)
```

### Step 12: Call _assert_view_allclose()

```python
_assert_view_allclose(brain, roll, distance, azimuth, elevation, focalpoint, align)
```

### Step 13: Assign unknown = value

```python
azimuth, elevation = (180.0, 90.0)
```

### Step 14: Call view_args.update()

```python
view_args.update(azimuth=azimuth, elevation=elevation)
```

### Step 15: Call brain.show_view()

```python
brain.show_view(**view_args)
```

### Step 16: Call _assert_view_allclose()

```python
_assert_view_allclose(brain, roll, distance, azimuth, elevation, focalpoint, align)
```

### Step 17: Call brain.close()

```python
brain.close()
```


## Complete Example

```python
# Setup
# Fixtures: renderer_interactive_pyvistaqt, tmp_path, brain_gc, align

# Workflow
'Test get_view / set_view round-trip.'
brain = _create_testing_brain(hemi='lh')
img = brain.screenshot()
roll, distance, azimuth, elevation, focalpoint = brain.get_view(align=align)
brain.show_view(azimuth=azimuth, elevation=elevation, focalpoint=focalpoint, roll=roll, distance=distance, align=align)
img_1 = brain.screenshot()
assert_allclose(img, img_1)
_assert_view_allclose(brain, roll, distance, azimuth, elevation, focalpoint, align)
roll, distance, focalpoint = (1, 500, (1e-05, 1e-05, 1e-05))
view_args = dict(roll=roll, distance=distance, focalpoint=focalpoint, align=align)
brain.show_view(**view_args)
_assert_view_allclose(brain, roll, distance, azimuth, elevation, focalpoint, align)
azimuth, elevation = (180.0, 90.0)
view_args.update(azimuth=azimuth, elevation=elevation)
brain.show_view(**view_args)
_assert_view_allclose(brain, roll, distance, azimuth, elevation, focalpoint, align)
brain.close()
```

## Next Steps


---

*Source: test_brain.py:710 | Complexity: Advanced | Last updated: 2026-05-18*