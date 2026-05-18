# How To: Plot Alignment Meg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plotting of MEG sensors + helmet.

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
# Fixtures: renderer, system
```

## Step-by-Step Guide

### Step 1: 'Test plotting of MEG sensors + helmet.'

```python
'Test plotting of MEG sensors + helmet.'
```

**Verification:**
```python
assert system == 'KIT'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert isinstance(fig, Figure3D)
```

### Step 3: Assign meg = value

```python
meg = {'helmet': 0.1, 'sensors': 0.2}
```

### Step 4: Assign sensor_colors = 'k'

```python
sensor_colors = 'k'
```

### Step 5: Assign fig = plot_alignment(...)

```python
fig = plot_alignment(this_info, read_trans(trans_fname), subject='sample', subjects_dir=subjects_dir, meg=meg, eeg=False, sensor_colors=sensor_colors)
```

**Verification:**
```python
assert isinstance(fig, Figure3D)
```

### Step 6: Assign use_info = pick_info(...)

```python
use_info = pick_info(this_info, pick_types(this_info, meg=True, eeg=False, ref_meg='ref' in meg, exclude=()))
```

### Step 7: Assign n_actors = value

```python
n_actors = use_info['nchan'] + 2
```

### Step 8: Call _assert_n_actors()

```python
_assert_n_actors(fig, renderer, n_actors)
```

### Step 9: Assign this_info = read_info(...)

```python
this_info = read_info(evoked_fname)
```

### Step 10: Assign unknown = 0.3

```python
meg['ref'] = 0.3
```

### Step 11: Assign sensor_colors = dict(...)

```python
sensor_colors = dict(meg=sensor_colors)
```

### Step 12: Assign unknown = value

```python
sensor_colors['ref_meg'] = ['r'] * len(pick_types(this_info, ref_meg=True))
```

### Step 13: Assign this_info = value

```python
this_info = read_raw_ctf(ctf_fname).info
```

### Step 14: Call plot_alignment()

```python
plot_alignment(this_info, meg=meg, sensor_colors=sensor_colors)
```

### Step 15: Assign this_info = value

```python
this_info = read_raw_bti(pdf_fname, config_fname, hs_fname, convert=True, preload=False).info
```

**Verification:**
```python
assert system == 'KIT'
```

### Step 16: Assign this_info = value

```python
this_info = read_raw_kit(sqd_fname).info
```


## Complete Example

```python
# Setup
# Fixtures: renderer, system

# Workflow
'Test plotting of MEG sensors + helmet.'
pytest.importorskip('nibabel')
if system == 'Neuromag':
    this_info = read_info(evoked_fname)
elif system == 'CTF':
    this_info = read_raw_ctf(ctf_fname).info
elif system == 'BTi':
    this_info = read_raw_bti(pdf_fname, config_fname, hs_fname, convert=True, preload=False).info
else:
    assert system == 'KIT'
    this_info = read_raw_kit(sqd_fname).info
meg = {'helmet': 0.1, 'sensors': 0.2}
sensor_colors = 'k'
if system == 'KIT':
    meg['ref'] = 0.3
    with pytest.raises(TypeError, match='instance of dict'):
        plot_alignment(this_info, meg=meg, sensor_colors=sensor_colors)
    sensor_colors = dict(meg=sensor_colors)
    sensor_colors['ref_meg'] = ['r'] * len(pick_types(this_info, ref_meg=True))
fig = plot_alignment(this_info, read_trans(trans_fname), subject='sample', subjects_dir=subjects_dir, meg=meg, eeg=False, sensor_colors=sensor_colors)
assert isinstance(fig, Figure3D)
use_info = pick_info(this_info, pick_types(this_info, meg=True, eeg=False, ref_meg='ref' in meg, exclude=()))
n_actors = use_info['nchan'] + 2
_assert_n_actors(fig, renderer, n_actors)
```

## Next Steps


---

*Source: test_3d.py:455 | Complexity: Advanced | Last updated: 2026-05-18*