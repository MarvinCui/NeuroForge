# How To: Plot Dipole Mri Outlines

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
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
# Fixtures: surf, coord_frame, ax, title
```

## Step-by-Step Guide

### Step 1: 'Test mpl dipole plotting.'

```python
'Test mpl dipole plotting.'
```

**Verification:**
```python
assert isinstance(ax, str) and ax == 'mpl', ax
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert isinstance(fig, Figure)
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
fig = dipoles.plot_locations(trans=trans, subject='sample', subjects_dir=subjects_dir, mode='outlines', coord_frame=coord_frame, surf=surf, ax=ax, title=title)
```

**Verification:**
```python
assert isinstance(fig, Figure)
```

### Step 6: Assign unknown = plt.subplots(...)

```python
_, ax = plt.subplots(3, 1)
```

### Step 7: Assign ax = list(...)

```python
ax = list(ax)
```

### Step 8: Call dipoles.plot_locations()

```python
dipoles.plot_locations(trans, 'sample', subjects_dir, ax=ax[:2], mode='outlines')
```


## Complete Example

```python
# Setup
# Fixtures: surf, coord_frame, ax, title

# Workflow
'Test mpl dipole plotting.'
pytest.importorskip('nibabel')
dipoles = read_dipole(dip_fname)
trans = read_trans(trans_fname)
if ax is not None:
    assert isinstance(ax, str) and ax == 'mpl', ax
    _, ax = plt.subplots(3, 1)
    ax = list(ax)
    with pytest.raises(ValueError, match='but the length is 2'):
        dipoles.plot_locations(trans, 'sample', subjects_dir, ax=ax[:2], mode='outlines')
fig = dipoles.plot_locations(trans=trans, subject='sample', subjects_dir=subjects_dir, mode='outlines', coord_frame=coord_frame, surf=surf, ax=ax, title=title)
assert isinstance(fig, Figure)
```

## Next Steps


---

*Source: test_3d.py:1157 | Complexity: Advanced | Last updated: 2026-05-18*