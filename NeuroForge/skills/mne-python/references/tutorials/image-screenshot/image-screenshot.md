# How To: Image Screenshot

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test screenshot and image saving.

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
# Fixtures: renderer_interactive_pyvistaqt, tmp_path, pixel_ratio, brain_gc
```

## Step-by-Step Guide

### Step 1: 'Test screenshot and image saving.'

```python
'Test screenshot and image saving.'
```

**Verification:**
```python
assert not fname.is_file()
```

### Step 2: Assign size = value

```python
size = (300, 300)
```

**Verification:**
```python
assert fname.is_file()
```

### Step 3: Assign brain = _create_testing_brain(...)

```python
brain = _create_testing_brain(hemi='rh', show_traces=False, size=size)
```

**Verification:**
```python
assert_allclose(a_, azimuth, atol=1e-06)
```

### Step 4: Assign unknown = value

```python
azimuth, elevation = (180.0, 90.0)
```

**Verification:**
```python
assert_allclose(e_, elevation)
```

### Step 5: Assign fname = value

```python
fname = tmp_path / 'test.png'
```

**Verification:**
```python
assert_allclose(f_, fp, atol=1e-06)
```

### Step 6: Call brain.save_image()

```python
brain.save_image(fname)
```

**Verification:**
```python
assert_allclose(img.shape, want_size, atol=15)
```

### Step 7: Assign fp = np.array(...)

```python
fp = np.array(brain._renderer.figure.plotter.renderer.ComputeVisiblePropBounds())
```

### Step 8: Assign fp = value

```python
fp = (fp[1::2] + fp[::2]) * 0.5
```

### Step 9: Assign img = brain.screenshot(...)

```python
img = brain.screenshot(mode='rgba')
```

### Step 10: Assign want_size = np.array(...)

```python
want_size = np.array([size[0] * pixel_ratio, size[1] * pixel_ratio, 4])
```

### Step 11: Assign div = value

```python
div = 2 if np.allclose(img.shape[:2], want_size[:2] / 2.0, atol=15) else 1
```

### Step 12: Call assert_allclose()

```python
assert_allclose(img.shape, want_size, atol=15)
```

### Step 13: Call brain.close()

```python
brain.close()
```

### Step 14: Call brain.show_view()

```python
brain.show_view(**view_args)
```

### Step 15: Assign unknown = brain.get_view(...)

```python
_, _, a_, e_, f_ = brain.get_view()
```

### Step 16: Call assert_allclose()

```python
assert_allclose(a_, azimuth, atol=1e-06)
```

### Step 17: Call assert_allclose()

```python
assert_allclose(e_, elevation)
```

### Step 18: Call assert_allclose()

```python
assert_allclose(f_, fp, atol=1e-06)
```


## Complete Example

```python
# Setup
# Fixtures: renderer_interactive_pyvistaqt, tmp_path, pixel_ratio, brain_gc

# Workflow
'Test screenshot and image saving.'
size = (300, 300)
brain = _create_testing_brain(hemi='rh', show_traces=False, size=size)
azimuth, elevation = (180.0, 90.0)
fname = tmp_path / 'test.png'
assert not fname.is_file()
brain.save_image(fname)
assert fname.is_file()
fp = np.array(brain._renderer.figure.plotter.renderer.ComputeVisiblePropBounds())
fp = (fp[1::2] + fp[::2]) * 0.5
for view_args in (dict(azimuth=azimuth, elevation=elevation, focalpoint='auto'), dict(view='lateral', hemi='rh')):
    brain.show_view(**view_args)
    _, _, a_, e_, f_ = brain.get_view()
    assert_allclose(a_, azimuth, atol=1e-06)
    assert_allclose(e_, elevation)
    assert_allclose(f_, fp, atol=1e-06)
img = brain.screenshot(mode='rgba')
want_size = np.array([size[0] * pixel_ratio, size[1] * pixel_ratio, 4])
div = 2 if np.allclose(img.shape[:2], want_size[:2] / 2.0, atol=15) else 1
want_size[:2] /= div
assert_allclose(img.shape, want_size, atol=15)
brain.close()
```

## Next Steps


---

*Source: test_brain.py:741 | Complexity: Advanced | Last updated: 2026-05-18*