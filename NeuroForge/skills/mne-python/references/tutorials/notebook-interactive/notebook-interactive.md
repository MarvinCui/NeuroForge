# How To: Notebook Interactive

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: mock, pytest

## Overview

Instantiate plot: Test interactive modes.

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

### Step 1: Assign brain = stc.plot(...)

```python
brain = stc.plot(subjects_dir=subjects_dir, initial_time=initial_time, clim=dict(kind='value', pos_lims=[3, 6, 9]), time_viewer=True, show_traces=True, hemi='lh', size=300)
```


## Complete Example

```python
# Setup
# Fixtures: renderer_notebook, brain_gc, nbexec

# Workflow
brain = stc.plot(subjects_dir=subjects_dir, initial_time=initial_time, clim=dict(kind='value', pos_lims=[3, 6, 9]), time_viewer=True, show_traces=True, hemi='lh', size=300)
```

## Next Steps


---

*Source: test_notebook.py:80 | Complexity: Beginner | Last updated: 2026-05-18*