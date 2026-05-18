# How To: Stc Mpl

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting source estimates with matplotlib.

## Prerequisites

**Required Modules:**
- `contextlib`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `matplotlib.figure`
- `numpy.testing`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.bem`
- `mne.datasets`
- `mne.defaults`
- `mne.fixes`
- `mne.io`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space`
- `mne.transforms`
- `mne.utils`
- `mne.viz`
- `mne.viz._3d`
- `mne.viz.utils`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.viz`


## Step-by-Step Guide

### Step 1: 'Test plotting source estimates with matplotlib.'

```python
'Test plotting source estimates with matplotlib.'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

### Step 3: Assign sample_src = read_source_spaces(...)

```python
sample_src = read_source_spaces(src_fname)
```

### Step 4: Assign vertices = value

```python
vertices = [s['vertno'] for s in sample_src]
```

### Step 5: Assign n_time = 5

```python
n_time = 5
```

### Step 6: Assign n_verts = sum(...)

```python
n_verts = sum((len(v) for v in vertices))
```

### Step 7: Assign stc_data = np.ones(...)

```python
stc_data = np.ones(n_verts * n_time)
```

### Step 8: Assign stc_data = _reshape_view(...)

```python
stc_data = _reshape_view(stc_data, (n_verts, n_time))
```

### Step 9: Assign stc = SourceEstimate(...)

```python
stc = SourceEstimate(stc_data, vertices, 1, 1, 'sample')
```

### Step 10: Call stc.plot()

```python
stc.plot(subjects_dir=subjects_dir, time_unit='s', views='ven', hemi='rh', smoothing_steps=7, subject='sample', backend='matplotlib', spacing='oct1', initial_time=0.001, colormap='Reds')
```

### Step 11: Assign fig = stc.plot(...)

```python
fig = stc.plot(subjects_dir=subjects_dir, time_unit='ms', views='dor', hemi='lh', smoothing_steps=7, subject='sample', backend='matplotlib', spacing='ico2', time_viewer=True, colormap='mne')
```

### Step 12: Assign time_viewer = value

```python
time_viewer = fig.time_viewer
```

### Step 13: Call _fake_click()

```python
_fake_click(time_viewer, time_viewer.axes[0], (0.5, 0.5))
```

### Step 14: Call _fake_keypress()

```python
_fake_keypress(time_viewer, 'ctrl+right')
```

### Step 15: Call _fake_keypress()

```python
_fake_keypress(time_viewer, 'left')
```

### Step 16: Call pytest.raises()

```python
pytest.raises(ValueError, stc.plot, subjects_dir=subjects_dir, hemi='both', subject='sample', backend='matplotlib')
```

### Step 17: Call pytest.raises()

```python
pytest.raises(ValueError, stc.plot, subjects_dir=subjects_dir, time_unit='ss', subject='sample', backend='matplotlib')
```


## Complete Example

```python
# Workflow
'Test plotting source estimates with matplotlib.'
pytest.importorskip('nibabel')
sample_src = read_source_spaces(src_fname)
vertices = [s['vertno'] for s in sample_src]
n_time = 5
n_verts = sum((len(v) for v in vertices))
stc_data = np.ones(n_verts * n_time)
stc_data = _reshape_view(stc_data, (n_verts, n_time))
stc = SourceEstimate(stc_data, vertices, 1, 1, 'sample')
stc.plot(subjects_dir=subjects_dir, time_unit='s', views='ven', hemi='rh', smoothing_steps=7, subject='sample', backend='matplotlib', spacing='oct1', initial_time=0.001, colormap='Reds')
fig = stc.plot(subjects_dir=subjects_dir, time_unit='ms', views='dor', hemi='lh', smoothing_steps=7, subject='sample', backend='matplotlib', spacing='ico2', time_viewer=True, colormap='mne')
time_viewer = fig.time_viewer
_fake_click(time_viewer, time_viewer.axes[0], (0.5, 0.5))
_fake_keypress(time_viewer, 'ctrl+right')
_fake_keypress(time_viewer, 'left')
pytest.raises(ValueError, stc.plot, subjects_dir=subjects_dir, hemi='both', subject='sample', backend='matplotlib')
pytest.raises(ValueError, stc.plot, subjects_dir=subjects_dir, time_unit='ss', subject='sample', backend='matplotlib')
```

## Next Steps


---

*Source: test_3d.py:1060 | Complexity: Advanced | Last updated: 2026-05-18*