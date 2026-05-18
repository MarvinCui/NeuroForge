# How To: Plot Evoked Field Notebook

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test plotting the evoked field inside a notebook.

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
# Fixtures: renderer_notebook, nbexec
```

## Step-by-Step Guide

### Step 1: 'Test plotting the evoked field inside a notebook.'

```python
'Test plotting the evoked field inside a notebook.'
```

**Verification:**
```python
assert isinstance(fig, EvokedField)
```

### Step 2: Call set_3d_backend()

```python
set_3d_backend('notebook')
```

**Verification:**
```python
assert isinstance(fig, Figure3D)
```

### Step 3: Assign evoked_fname = value

```python
evoked_fname = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-ave.fif'
```

### Step 4: Assign trans_fname = value

```python
trans_fname = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-trans.fif'
```

### Step 5: Assign subjects_dir = value

```python
subjects_dir = data_path / 'subjects'
```

### Step 6: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(evoked_fname, condition='Left Auditory', baseline=(-0.2, 0.0))
```

### Step 7: Call evoked.pick()

```python
evoked.pick(evoked.ch_names[::10])
```

### Step 8: Assign fig = evoked.plot_field(...)

```python
fig = evoked.plot_field(maps, time_viewer=True)
```

**Verification:**
```python
assert isinstance(fig, EvokedField)
```

### Step 9: Assign fig = evoked.plot_field(...)

```python
fig = evoked.plot_field(maps, time_viewer=False)
```

**Verification:**
```python
assert isinstance(fig, Figure3D)
```

### Step 10: Assign brain = Brain(...)

```python
brain = Brain('fsaverage', 'lh', 'inflated', subjects_dir=subjects_dir)
```

### Step 11: Call mp.delenv()

```python
mp.delenv('_MNE_FAKE_HOME_DIR')
```

### Step 12: Assign data_path = testing.data_path(...)

```python
data_path = testing.data_path(download=False)
```

### Step 13: Assign maps = make_field_map(...)

```python
maps = make_field_map(evoked, trans_fname, subject='sample', subjects_dir=subjects_dir, n_jobs=None, ch_type='meg')
```

### Step 14: Assign fig = evoked.plot_field(...)

```python
fig = evoked.plot_field(maps, time=0.1, fig=brain)
```


## Complete Example

```python
# Setup
# Fixtures: renderer_notebook, nbexec

# Workflow
'Test plotting the evoked field inside a notebook.'
import pytest
from mne import make_field_map, read_evokeds
from mne.datasets import testing
from mne.viz import Brain, EvokedField, Figure3D, set_3d_backend
set_3d_backend('notebook')
with pytest.MonkeyPatch().context() as mp:
    mp.delenv('_MNE_FAKE_HOME_DIR')
    data_path = testing.data_path(download=False)
evoked_fname = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-ave.fif'
trans_fname = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-trans.fif'
subjects_dir = data_path / 'subjects'
evoked = read_evokeds(evoked_fname, condition='Left Auditory', baseline=(-0.2, 0.0))
evoked.pick(evoked.ch_names[::10])
with pytest.warns(RuntimeWarning, match='projection'):
    maps = make_field_map(evoked, trans_fname, subject='sample', subjects_dir=subjects_dir, n_jobs=None, ch_type='meg')
fig = evoked.plot_field(maps, time_viewer=True)
assert isinstance(fig, EvokedField)
fig = evoked.plot_field(maps, time_viewer=False)
assert isinstance(fig, Figure3D)
brain = Brain('fsaverage', 'lh', 'inflated', subjects_dir=subjects_dir)
with pytest.raises(NotImplementedError):
    fig = evoked.plot_field(maps, time=0.1, fig=brain)
```

## Next Steps


---

*Source: test_3d.py:242 | Complexity: Advanced | Last updated: 2026-05-18*