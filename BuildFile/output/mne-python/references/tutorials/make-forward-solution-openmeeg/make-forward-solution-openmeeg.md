# How To: Make Forward Solution Openmeeg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test making M-EEG forward solution from OpenMEEG.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.datasets`
- `mne.dipole`
- `mne.forward`
- `mne.forward._compute_forward`
- `mne.forward._make_forward`
- `mne.forward.tests.test_forward`
- `mne.io`
- `mne.simulation`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: n_layers
```

## Step-by-Step Guide

### Step 1: 'Test making M-EEG forward solution from OpenMEEG.'

```python
'Test making M-EEG forward solution from OpenMEEG.'
```

**Verification:**
```python
assert bem_surfaces[0]['id'] == FIFF.FIFFV_BEM_SURF_ID_BRAIN
```

### Step 2: Assign solver = 'openmeeg'

```python
solver = 'openmeeg'
```

**Verification:**
```python
assert bem['solver'] == solver
```

### Step 3: Assign bem_surfaces = read_bem_surfaces(...)

```python
bem_surfaces = read_bem_surfaces(fname_bem)
```

**Verification:**
```python
assert 'Total 258/258 points inside the surface' in log
```

### Step 4: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw)
```

**Verification:**
```python
assert isinstance(fwd, Forward)
```

### Step 5: Assign n_sensors = 366

```python
n_sensors = 366
```

### Step 6: Assign ch_types = value

```python
ch_types = ['eeg', 'meg']
```

### Step 7: Call raw.pick()

```python
raw.pick(ch_types)
```

### Step 8: Assign n_sources_kept = value

```python
n_sources_kept = 501 // 3
```

### Step 9: Assign fwds = dict(...)

```python
fwds = dict()
```

### Step 10: Call _compare_forwards()

```python
_compare_forwards(fwds['openmeeg'], fwds['mne'], n_sensors, n_sources_kept * 3, meg_atol=1, eeg_atol=100, meg_corr_tol=0.98, eeg_corr_tol=0.98, meg_rdm_tol=0.11, eeg_rdm_tol=0.2)
```

### Step 11: Assign ch_types = value

```python
ch_types = ['meg']
```

### Step 12: Assign bem_surfaces = value

```python
bem_surfaces = bem_surfaces[-1:]
```

**Verification:**
```python
assert bem_surfaces[0]['id'] == FIFF.FIFFV_BEM_SURF_ID_BRAIN
```

### Step 13: Assign n_sensors = 306

```python
n_sensors = 306
```

### Step 14: Assign bem = make_bem_solution(...)

```python
bem = make_bem_solution(bem_surfaces, solver=solver)
```

**Verification:**
```python
assert bem['solver'] == solver
```

### Step 15: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'Total 258/258 points inside the surface' in log
```

### Step 16: Assign unknown = fwd

```python
fwds[solver] = fwd
```

### Step 17: Assign fwd = make_forward_solution(...)

```python
fwd = make_forward_solution(raw.info, Path(fname_trans), Path(fname_src), bem, mindist=20.0, verbose=True)
```


## Complete Example

```python
# Setup
# Fixtures: n_layers

# Workflow
'Test making M-EEG forward solution from OpenMEEG.'
solver = 'openmeeg'
bem_surfaces = read_bem_surfaces(fname_bem)
raw = read_raw_fif(fname_raw)
n_sensors = 366
ch_types = ['eeg', 'meg']
if n_layers == 1:
    ch_types = ['meg']
    bem_surfaces = bem_surfaces[-1:]
    assert bem_surfaces[0]['id'] == FIFF.FIFFV_BEM_SURF_ID_BRAIN
    n_sensors = 306
raw.pick(ch_types)
n_sources_kept = 501 // 3
fwds = dict()
for solver in ['openmeeg', 'mne']:
    bem = make_bem_solution(bem_surfaces, solver=solver)
    assert bem['solver'] == solver
    with catch_logging() as log:
        fwd = make_forward_solution(raw.info, Path(fname_trans), Path(fname_src), bem, mindist=20.0, verbose=True)
    log = log.getvalue()
    assert 'Total 258/258 points inside the surface' in log
    assert isinstance(fwd, Forward)
    fwds[solver] = fwd
    del fwd
_compare_forwards(fwds['openmeeg'], fwds['mne'], n_sensors, n_sources_kept * 3, meg_atol=1, eeg_atol=100, meg_corr_tol=0.98, eeg_corr_tol=0.98, meg_rdm_tol=0.11, eeg_rdm_tol=0.2)
```

## Next Steps


---

*Source: test_make_forward.py:451 | Complexity: Advanced | Last updated: 2026-05-18*