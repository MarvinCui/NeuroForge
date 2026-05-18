# How To: Brain Save Movie

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test saving a movie of a Brain instance.

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
# Fixtures: tmp_path, renderer, brain_gc, interactive_state
```

## Step-by-Step Guide

### Step 1: 'Test saving a movie of a Brain instance.'

```python
'Test saving a movie of a Brain instance.'
```

**Verification:**
```python
assert not filename.is_file()
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('imageio')
```

**Verification:**
```python
assert filename.is_file()
```

### Step 3: Assign imageio_ffmpeg = pytest.importorskip(...)

```python
imageio_ffmpeg = pytest.importorskip('imageio_ffmpeg')
```

**Verification:**
```python
assert_allclose(duration, nsecs, atol=0.2)
```

### Step 4: Assign brain = _create_testing_brain(...)

```python
brain = _create_testing_brain(hemi='lh', time_viewer=False, cortex=['r', 'b'])
```

### Step 5: Assign filename = value

```python
filename = tmp_path / 'brain_test.mov'
```

**Verification:**
```python
assert not filename.is_file()
```

### Step 6: Assign tmin = 1

```python
tmin = 1
```

### Step 7: Assign tmax = 5

```python
tmax = 5
```

### Step 8: Assign duration = np.floor(...)

```python
duration = np.floor(tmax - tmin)
```

### Step 9: Call brain.save_movie()

```python
brain.save_movie(filename, time_dilation=1.0, tmin=tmin, tmax=tmax, interpolation='nearest')
```

**Verification:**
```python
assert filename.is_file()
```

### Step 10: Assign unknown = imageio_ffmpeg.count_frames_and_secs(...)

```python
_, nsecs = imageio_ffmpeg.count_frames_and_secs(filename)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(duration, nsecs, atol=0.2)
```

### Step 12: Call os.remove()

```python
os.remove(filename)
```

### Step 13: Call brain.close()

```python
brain.close()
```

### Step 14: Call brain._renderer.plotter.enable()

```python
brain._renderer.plotter.enable()
```

### Step 15: Call brain._renderer.plotter.disable()

```python
brain._renderer.plotter.disable()
```

### Step 16: Call brain.save_movie()

```python
brain.save_movie(filename, time_dilation=1, tmin=1, tmax=1.1, bad_name='blah')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, renderer, brain_gc, interactive_state

# Workflow
'Test saving a movie of a Brain instance.'
pytest.importorskip('imageio')
imageio_ffmpeg = pytest.importorskip('imageio_ffmpeg')
brain = _create_testing_brain(hemi='lh', time_viewer=False, cortex=['r', 'b'])
filename = tmp_path / 'brain_test.mov'
try:
    if interactive_state:
        brain._renderer.plotter.enable()
    else:
        brain._renderer.plotter.disable()
    with pytest.raises(TypeError, match='unexpected keyword argument'):
        brain.save_movie(filename, time_dilation=1, tmin=1, tmax=1.1, bad_name='blah')
    assert not filename.is_file()
    tmin = 1
    tmax = 5
    duration = np.floor(tmax - tmin)
    brain.save_movie(filename, time_dilation=1.0, tmin=tmin, tmax=tmax, interpolation='nearest')
    assert filename.is_file()
    _, nsecs = imageio_ffmpeg.count_frames_and_secs(filename)
    assert_allclose(duration, nsecs, atol=0.2)
    os.remove(filename)
finally:
    brain.close()
```

## Next Steps


---

*Source: test_brain.py:802 | Complexity: Advanced | Last updated: 2026-05-18*