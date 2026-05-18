# How To: Plot Sparse Source Estimates

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plotting of (sparse) source estimates.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: renderer_interactive, brain_gc
```

## Step-by-Step Guide

### Step 1: 'Test plotting of (sparse) source estimates.'

```python
'Test plotting of (sparse) source estimates.'
```

**Verification:**
```python
assert isinstance(out, Figure3D)
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

### Step 7: Assign stc_data = np.zeros(...)

```python
stc_data = np.zeros(n_verts * n_time)
```

### Step 8: Assign stc_size = value

```python
stc_size = stc_data.size
```

### Step 9: Assign unknown = np.random.RandomState.rand(...)

```python
stc_data[(np.random.rand(stc_size // 20) * stc_size).astype(int)] = np.random.RandomState(0).rand(stc_data.size // 20)
```

### Step 10: Assign stc_data = _reshape_view(...)

```python
stc_data = _reshape_view(stc_data, (n_verts, n_time))
```

### Step 11: Assign stc = SourceEstimate(...)

```python
stc = SourceEstimate(stc_data, vertices, 1, 1)
```

### Step 12: Assign colormap = 'mne_analyze'

```python
colormap = 'mne_analyze'
```

### Step 13: Assign brain = plot_source_estimates(...)

```python
brain = plot_source_estimates(stc, 'sample', colormap=colormap, background=(1, 1, 0), subjects_dir=subjects_dir, colorbar=True, clim='auto')
```

### Step 14: Call brain.close()

```python
brain.close()
```

### Step 15: Assign vertices = value

```python
vertices = sample_src[0]['vertno']
```

### Step 16: Assign inds = value

```python
inds = [111, 333]
```

### Step 17: Assign stc_data = np.zeros(...)

```python
stc_data = np.zeros((len(inds), n_time))
```

### Step 18: Assign unknown = 1.0

```python
stc_data[0, 1] = 1.0
```

### Step 19: Assign unknown = 2.0

```python
stc_data[1, 4] = 2.0
```

### Step 20: Assign vertices = value

```python
vertices = [vertices[inds], np.empty(0, dtype=np.int64)]
```

### Step 21: Assign stc = SourceEstimate(...)

```python
stc = SourceEstimate(stc_data, vertices, 1, 1)
```

### Step 22: Assign out = plot_sparse_source_estimates(...)

```python
out = plot_sparse_source_estimates(sample_src, stc, bgcolor=(1, 1, 1), opacity=0.5, high_resolution=False)
```

**Verification:**
```python
assert isinstance(out, Figure3D)
```

### Step 23: Call plot_source_estimates()

```python
plot_source_estimates(stc, 'sample', figure='foo', hemi='both', clim='auto', subjects_dir=subjects_dir)
```


## Complete Example

```python
# Setup
# Fixtures: renderer_interactive, brain_gc

# Workflow
'Test plotting of (sparse) source estimates.'
pytest.importorskip('nibabel')
sample_src = read_source_spaces(src_fname)
vertices = [s['vertno'] for s in sample_src]
n_time = 5
n_verts = sum((len(v) for v in vertices))
stc_data = np.zeros(n_verts * n_time)
stc_size = stc_data.size
stc_data[(np.random.rand(stc_size // 20) * stc_size).astype(int)] = np.random.RandomState(0).rand(stc_data.size // 20)
stc_data = _reshape_view(stc_data, (n_verts, n_time))
stc = SourceEstimate(stc_data, vertices, 1, 1)
colormap = 'mne_analyze'
brain = plot_source_estimates(stc, 'sample', colormap=colormap, background=(1, 1, 0), subjects_dir=subjects_dir, colorbar=True, clim='auto')
brain.close()
del brain
with pytest.raises(TypeError, match='figure must be'):
    plot_source_estimates(stc, 'sample', figure='foo', hemi='both', clim='auto', subjects_dir=subjects_dir)
vertices = sample_src[0]['vertno']
inds = [111, 333]
stc_data = np.zeros((len(inds), n_time))
stc_data[0, 1] = 1.0
stc_data[1, 4] = 2.0
vertices = [vertices[inds], np.empty(0, dtype=np.int64)]
stc = SourceEstimate(stc_data, vertices, 1, 1)
out = plot_sparse_source_estimates(sample_src, stc, bgcolor=(1, 1, 1), opacity=0.5, high_resolution=False)
assert isinstance(out, Figure3D)
```

## Next Steps


---

*Source: test_3d.py:125 | Complexity: Advanced | Last updated: 2026-05-18*