# How To: Calculate Head Pos Chpi On Chpi5 In One Second Steps

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Comparing estimated cHPI positions with MF results (one second).

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

### Step 1: 'Comparing estimated cHPI positions with MF results (one second).'

```python
'Comparing estimated cHPI positions with MF results (one second).'
```

### Step 2: Assign mf_quats = read_head_pos(...)

```python
mf_quats = read_head_pos(chpi5_pos_fname)
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(chpi5_fif_fname, allow_maxshield='yes')
```

### Step 4: Assign raw = _decimate_chpi(...)

```python
raw = _decimate_chpi(raw.crop(0.0, 10.0).load_data(), decim=8)
```

### Step 5: Assign py_quats = _calculate_chpi_positions(...)

```python
py_quats = _calculate_chpi_positions(raw, t_step_min=1.0, t_step_max=1.0, t_window=1.0, verbose='debug')
```

### Step 6: Call _assert_quats()

```python
_assert_quats(py_quats, mf_quats, dist_tol=0.002, angle_tol=1.2, vel_atol=0.003)
```


## Complete Example

```python
# Workflow
'Comparing estimated cHPI positions with MF results (one second).'
mf_quats = read_head_pos(chpi5_pos_fname)
raw = read_raw_fif(chpi5_fif_fname, allow_maxshield='yes')
raw = _decimate_chpi(raw.crop(0.0, 10.0).load_data(), decim=8)
py_quats = _calculate_chpi_positions(raw, t_step_min=1.0, t_step_max=1.0, t_window=1.0, verbose='debug')
_assert_quats(py_quats, mf_quats, dist_tol=0.002, angle_tol=1.2, vel_atol=0.003)
```

## Next Steps


---

*Source: test_chpi.py:490 | Complexity: Intermediate | Last updated: 2026-05-18*