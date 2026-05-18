# How To: Make Forward Solution Discrete

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test making and converting a forward solution with discrete src.

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
# Fixtures: tmp_path, small_surf_src
```

## Step-by-Step Guide

### Step 1: 'Test making and converting a forward solution with discrete src.'

```python
'Test making and converting a forward solution with discrete src.'
```

### Step 2: Assign src = small_surf_src

```python
src = small_surf_src
```

### Step 3: Assign src = value

```python
src = src + setup_volume_source_space(pos=dict(rr=src[0]['rr'][src[0]['vertno'][:3]].copy(), nn=src[0]['nn'][src[0]['vertno'][:3]].copy()))
```

### Step 4: Assign sphere = make_sphere_model(...)

```python
sphere = make_sphere_model()
```

### Step 5: Assign fwd = make_forward_solution(...)

```python
fwd = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=False)
```

### Step 6: Call convert_forward_solution()

```python
convert_forward_solution(fwd, surf_ori=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, small_surf_src

# Workflow
'Test making and converting a forward solution with discrete src.'
src = small_surf_src
src = src + setup_volume_source_space(pos=dict(rr=src[0]['rr'][src[0]['vertno'][:3]].copy(), nn=src[0]['nn'][src[0]['vertno'][:3]].copy()))
sphere = make_sphere_model()
fwd = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=False)
convert_forward_solution(fwd, surf_ori=True)
```

## Next Steps


---

*Source: test_make_forward.py:498 | Complexity: Intermediate | Last updated: 2026-05-18*