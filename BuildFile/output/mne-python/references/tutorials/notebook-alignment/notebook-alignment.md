# How To: Notebook Alignment

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test plot alignment in a notebook.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `mne.datasets`
- `pytest`
- `mne`
- `tempfile`
- `time`
- `contextlib`
- `pathlib`
- `matplotlib.pyplot`
- `pytest`
- `ipywidgets`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `ipywidgets`
- `mne`

**Setup Required:**
```python
# Fixtures: renderer_notebook, brain_gc, nbexec
```

## Step-by-Step Guide

### Step 1: 'Test plot alignment in a notebook.'

```python
'Test plot alignment in a notebook.'
```

**Verification:**
```python
assert fig.display is not None
```

### Step 2: Assign raw_fname = value

```python
raw_fname = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc_raw.fif'
```

### Step 3: Assign subjects_dir = value

```python
subjects_dir = data_path / 'subjects'
```

### Step 4: Assign subject = 'sample'

```python
subject = 'sample'
```

### Step 5: Assign trans = value

```python
trans = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-trans.fif'
```

### Step 6: Assign info = mne.io.read_info(...)

```python
info = mne.io.read_info(raw_fname)
```

### Step 7: Call mne.viz.set_3d_backend()

```python
mne.viz.set_3d_backend('notebook')
```

### Step 8: Assign fig = mne.viz.plot_alignment(...)

```python
fig = mne.viz.plot_alignment(info, trans, subject=subject, dig=True, meg=['helmet', 'sensors'], subjects_dir=subjects_dir, surfaces=['head-dense'])
```

**Verification:**
```python
assert fig.display is not None
```

### Step 9: Call mp.delenv()

```python
mp.delenv('_MNE_FAKE_HOME_DIR')
```

### Step 10: Assign data_path = mne.datasets.testing.data_path(...)

```python
data_path = mne.datasets.testing.data_path(download=False)
```


## Complete Example

```python
# Setup
# Fixtures: renderer_notebook, brain_gc, nbexec

# Workflow
'Test plot alignment in a notebook.'
import pytest
import mne
with pytest.MonkeyPatch().context() as mp:
    mp.delenv('_MNE_FAKE_HOME_DIR')
    data_path = mne.datasets.testing.data_path(download=False)
raw_fname = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc_raw.fif'
subjects_dir = data_path / 'subjects'
subject = 'sample'
trans = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-trans.fif'
info = mne.io.read_info(raw_fname)
mne.viz.set_3d_backend('notebook')
fig = mne.viz.plot_alignment(info, trans, subject=subject, dig=True, meg=['helmet', 'sensors'], subjects_dir=subjects_dir, surfaces=['head-dense'])
assert fig.display is not None
```

## Next Steps


---

*Source: test_notebook.py:14 | Complexity: Advanced | Last updated: 2026-05-18*