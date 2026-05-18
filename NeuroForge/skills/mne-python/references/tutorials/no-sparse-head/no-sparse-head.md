# How To: No Sparse Head

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test mne.gui.coregistration with no sparse head.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `contextlib`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.utils`
- `mne.viz`
- `mne.gui`
- `mne.gui`
- `mne.gui`
- `mne.gui`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.gui`
- `mne.gui`
- `mne.gui`

**Setup Required:**
```python
# Fixtures: subjects_dir_tmp, renderer_interactive_pyvistaqt, monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test mne.gui.coregistration with no sparse head.'

```python
'Test mne.gui.coregistration with no sparse head.'
```

### Step 2: Assign subjects_dir_tmp = Path(...)

```python
subjects_dir_tmp = Path(subjects_dir_tmp)
```

### Step 3: Assign subject = 'sample'

```python
subject = 'sample'
```

### Step 4: Assign unknown = mne.read_surface(...)

```python
out_rr, out_tris = mne.read_surface(subjects_dir_tmp / subject / 'bem' / 'outer_skin.surf')
```

### Step 5: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne.coreg, 'decimate_surface', lambda rr, tris, n_triangles: (out_rr, out_tris))
```

### Step 6: Call coreg.close()

```python
coreg.close()
```

### Step 7: Call os.remove()

```python
os.remove(subjects_dir_tmp / subject / 'bem' / head)
```

### Step 8: Assign coreg = coregistration(...)

```python
coreg = coregistration(inst=raw_path, subject=subject, subjects_dir=subjects_dir_tmp)
```


## Complete Example

```python
# Setup
# Fixtures: subjects_dir_tmp, renderer_interactive_pyvistaqt, monkeypatch

# Workflow
'Test mne.gui.coregistration with no sparse head.'
from mne.gui import coregistration
subjects_dir_tmp = Path(subjects_dir_tmp)
subject = 'sample'
out_rr, out_tris = mne.read_surface(subjects_dir_tmp / subject / 'bem' / 'outer_skin.surf')
for head in ('sample-head.fif', 'outer_skin.surf'):
    os.remove(subjects_dir_tmp / subject / 'bem' / head)
monkeypatch.setattr(mne.coreg, 'decimate_surface', lambda rr, tris, n_triangles: (out_rr, out_tris))
with pytest.warns(RuntimeWarning, match='No low-resolution head found'):
    coreg = coregistration(inst=raw_path, subject=subject, subjects_dir=subjects_dir_tmp)
coreg.close()
```

## Next Steps


---

*Source: test_coreg.py:362 | Complexity: Advanced | Last updated: 2026-05-18*