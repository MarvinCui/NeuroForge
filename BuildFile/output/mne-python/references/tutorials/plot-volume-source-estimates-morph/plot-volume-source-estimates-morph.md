# How To: Plot Volume Source Estimates Morph

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test interactive plotting of volume source estimates with morph.

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.minimum_norm`
- `mne.utils`
- `mne.viz`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test interactive plotting of volume source estimates with morph.'

```python
'Test interactive plotting of volume source estimates with morph.'
```

**Verification:**
```python
assert 't = 1.000 s' in log
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert '(-52.0, -8.0, -7.0) mm' in log
```

### Step 3: Call pytest.importorskip()

```python
pytest.importorskip('dipy')
```

### Step 4: Call pytest.importorskip()

```python
pytest.importorskip('nilearn')
```

### Step 5: Assign forward = read_forward_solution(...)

```python
forward = read_forward_solution(fwd_fname)
```

### Step 6: Assign sample_src = value

```python
sample_src = forward['src']
```

### Step 7: Assign vertices = value

```python
vertices = [s['vertno'] for s in sample_src]
```

### Step 8: Assign n_verts = sum(...)

```python
n_verts = sum((len(v) for v in vertices))
```

### Step 9: Assign n_time = 2

```python
n_time = 2
```

### Step 10: Assign data = np.random.RandomState.rand(...)

```python
data = np.random.RandomState(0).rand(n_verts, n_time)
```

### Step 11: Assign stc = VolSourceEstimate(...)

```python
stc = VolSourceEstimate(data, vertices, 1, 1)
```

### Step 12: Assign unknown = 'sample'

```python
sample_src[0]['subject_his_id'] = 'sample'
```

### Step 13: Assign morph = compute_source_morph(...)

```python
morph = compute_source_morph(sample_src, 'sample', 'fsaverage', zooms=5, subjects_dir=subjects_dir)
```

### Step 14: Assign initial_pos = value

```python
initial_pos = (-0.05, -0.01, -0.006)
```

### Step 15: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 't = 1.000 s' in log
```

### Step 16: Call vertices.append()

```python
vertices.append([])
```

### Step 17: Assign surface_stc = SourceEstimate(...)

```python
surface_stc = SourceEstimate(data, vertices, 1, 1)
```

### Step 18: Call stc.plot()

```python
stc.plot(sample_src, 'sample', subjects_dir, mode='abcd')
```

### Step 19: Call plot_volume_source_estimates()

```python
plot_volume_source_estimates(surface_stc, sample_src, 'sample', subjects_dir)
```

### Step 20: Call stc.plot()

```python
stc.plot(sample_src, 'sample', subjects_dir, clim=dict(lims=[-1, 2, 3], kind='value'))
```

### Step 21: Call stc.plot()

```python
stc.plot(morph, subjects_dir=subjects_dir, mode='glass_brain', initial_pos=initial_pos, verbose=True)
```


## Complete Example

```python
# Workflow
'Test interactive plotting of volume source estimates with morph.'
pytest.importorskip('nibabel')
pytest.importorskip('dipy')
pytest.importorskip('nilearn')
forward = read_forward_solution(fwd_fname)
sample_src = forward['src']
vertices = [s['vertno'] for s in sample_src]
n_verts = sum((len(v) for v in vertices))
n_time = 2
data = np.random.RandomState(0).rand(n_verts, n_time)
stc = VolSourceEstimate(data, vertices, 1, 1)
sample_src[0]['subject_his_id'] = 'sample'
morph = compute_source_morph(sample_src, 'sample', 'fsaverage', zooms=5, subjects_dir=subjects_dir)
initial_pos = (-0.05, -0.01, -0.006)
with _record_warnings():
    with catch_logging() as log:
        stc.plot(morph, subjects_dir=subjects_dir, mode='glass_brain', initial_pos=initial_pos, verbose=True)
log = log.getvalue()
assert 't = 1.000 s' in log
assert '(-52.0, -8.0, -7.0) mm' in log
with pytest.raises(ValueError, match='Allowed values are'):
    stc.plot(sample_src, 'sample', subjects_dir, mode='abcd')
vertices.append([])
surface_stc = SourceEstimate(data, vertices, 1, 1)
with pytest.raises(TypeError, match='an instance of VolSourceEstimate'):
    plot_volume_source_estimates(surface_stc, sample_src, 'sample', subjects_dir)
with pytest.raises(ValueError, match='Negative colormap limits'):
    stc.plot(sample_src, 'sample', subjects_dir, clim=dict(lims=[-1, 2, 3], kind='value'))
```

## Next Steps


---

*Source: test_3d_mpl.py:113 | Complexity: Advanced | Last updated: 2026-05-18*