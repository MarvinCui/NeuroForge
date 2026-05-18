# How To: Plot Dipole Mri Orthoview

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test mpl dipole plotting.

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
# Fixtures: coord_frame, idx, show_all, title
```

## Step-by-Step Guide

### Step 1: 'Test mpl dipole plotting.'

```python
'Test mpl dipole plotting.'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

### Step 3: Assign dipoles = read_dipole(...)

```python
dipoles = read_dipole(dip_fname)
```

### Step 4: Assign trans = read_trans(...)

```python
trans = read_trans(trans_fname)
```

### Step 5: Assign fig = dipoles.plot_locations(...)

```python
fig = dipoles.plot_locations(trans=trans, subject='sample', subjects_dir=subjects_dir, coord_frame=coord_frame, idx=idx, show_all=show_all, title=title, mode='orthoview')
```

### Step 6: Call _fake_scroll()

```python
_fake_scroll(fig, 0.5, 0.5, 1)
```

### Step 7: Call _fake_scroll()

```python
_fake_scroll(fig, 0.5, 0.5, -1)
```

### Step 8: Call _fake_keypress()

```python
_fake_keypress(fig, 'up')
```

### Step 9: Call _fake_keypress()

```python
_fake_keypress(fig, 'down')
```

### Step 10: Call _fake_keypress()

```python
_fake_keypress(fig, 'a')
```

### Step 11: Assign ax = fig.add_subplot(...)

```python
ax = fig.add_subplot(211)
```

### Step 12: Call dipoles.plot_locations()

```python
dipoles.plot_locations(trans, 'sample', subjects_dir, ax=ax)
```


## Complete Example

```python
# Setup
# Fixtures: coord_frame, idx, show_all, title

# Workflow
'Test mpl dipole plotting.'
pytest.importorskip('nibabel')
dipoles = read_dipole(dip_fname)
trans = read_trans(trans_fname)
fig = dipoles.plot_locations(trans=trans, subject='sample', subjects_dir=subjects_dir, coord_frame=coord_frame, idx=idx, show_all=show_all, title=title, mode='orthoview')
_fake_scroll(fig, 0.5, 0.5, 1)
_fake_scroll(fig, 0.5, 0.5, -1)
_fake_keypress(fig, 'up')
_fake_keypress(fig, 'down')
_fake_keypress(fig, 'a')
ax = fig.add_subplot(211)
with pytest.raises(TypeError, match='instance of Axes3D'):
    dipoles.plot_locations(trans, 'sample', subjects_dir, ax=ax)
```

## Next Steps


---

*Source: test_3d.py:1123 | Complexity: Advanced | Last updated: 2026-05-18*