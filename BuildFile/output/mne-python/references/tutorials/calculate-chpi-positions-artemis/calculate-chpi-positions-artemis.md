# How To: Calculate Chpi Positions Artemis

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test on 5k artemis data.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.interpolate`
- `scipy.spatial.distance`
- `mne`
- `mne._fiff.constants`
- `mne.chpi`
- `mne.datasets`
- `mne.forward._compute_forward`
- `mne.io`
- `mne.simulation`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz`
- `scipy.signal`


## Step-by-Step Guide

### Step 1: 'Test on 5k artemis data.'

```python
'Test on 5k artemis data.'
```

### Step 2: Assign raw = read_raw_artemis123(...)

```python
raw = read_raw_artemis123(art_fname, preload=True)
```

### Step 3: Assign mf_quats = read_head_pos(...)

```python
mf_quats = read_head_pos(art_mc_fname)
```

### Step 4: Assign py_quats = _calculate_chpi_positions(...)

```python
py_quats = _calculate_chpi_positions(raw, t_step_min=2.0, verbose='debug')
```

### Step 5: Call _assert_quats()

```python
_assert_quats(py_quats, mf_quats, dist_tol=0.001, angle_tol=1.0, err_rtol=0.7, vel_atol=0.01)
```


## Complete Example

```python
# Workflow
'Test on 5k artemis data.'
raw = read_raw_artemis123(art_fname, preload=True)
mf_quats = read_head_pos(art_mc_fname)
mf_quats[:, 8:] /= 100
py_quats = _calculate_chpi_positions(raw, t_step_min=2.0, verbose='debug')
_assert_quats(py_quats, mf_quats, dist_tol=0.001, angle_tol=1.0, err_rtol=0.7, vel_atol=0.01)
```

## Next Steps


---

*Source: test_chpi.py:426 | Complexity: Intermediate | Last updated: 2026-05-18*