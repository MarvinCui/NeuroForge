# How To: Plot Alignment Fnirs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test fNIRS plotting.

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
# Fixtures: renderer, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test fNIRS plotting.'

```python
'Test fNIRS plotting.'
```

**Verification:**
```python
assert info['nchan'] == 26
```

### Step 2: Assign info = value

```python
info = read_raw_nirx(nirx_fname).info
```

**Verification:**
```python
assert f"fnirs_cw_amplitude: {info['nchan']}" in log
```

### Step 3: Assign kwargs = dict(...)

```python
kwargs = dict(trans='fsaverage', subject='fsaverage', surfaces=(), verbose=True, subjects_dir=tmp_path)
```

### Step 4: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert f"fnirs_cw_amplitude: {info['nchan']}" in log
```

### Step 5: Call _assert_n_actors()

```python
_assert_n_actors(fig, renderer, info['nchan'])
```

### Step 6: Assign fig = plot_alignment(...)

```python
fig = plot_alignment(info, fnirs=['channels', 'sources', 'detectors'], **kwargs)
```

### Step 7: Call _assert_n_actors()

```python
_assert_n_actors(fig, renderer, 3)
```

### Step 8: Assign fig = plot_alignment(...)

```python
fig = plot_alignment(info, **kwargs)
```


## Complete Example

```python
# Setup
# Fixtures: renderer, tmp_path

# Workflow
'Test fNIRS plotting.'
info = read_raw_nirx(nirx_fname).info
assert info['nchan'] == 26
kwargs = dict(trans='fsaverage', subject='fsaverage', surfaces=(), verbose=True, subjects_dir=tmp_path)
with catch_logging() as log:
    fig = plot_alignment(info, **kwargs)
log = log.getvalue()
assert f"fnirs_cw_amplitude: {info['nchan']}" in log
_assert_n_actors(fig, renderer, info['nchan'])
fig = plot_alignment(info, fnirs=['channels', 'sources', 'detectors'], **kwargs)
_assert_n_actors(fig, renderer, 3)
```

## Next Steps


---

*Source: test_3d.py:904 | Complexity: Advanced | Last updated: 2026-05-18*