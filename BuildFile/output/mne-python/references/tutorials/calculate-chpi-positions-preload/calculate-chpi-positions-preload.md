# How To: Calculate Chpi Positions Preload

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test calculation of cHPI positions with and without data loaded.

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

### Step 1: 'Test calculation of cHPI positions with and without data loaded.'

```python
'Test calculation of cHPI positions with and without data loaded.'
```

**Verification:**
```python
assert object_diff(pos, pos_preload) == ''
```

### Step 2: Assign raw = read_raw_fif.crop(...)

```python
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes').crop(0, 2)
```

### Step 3: Assign kwargs = dict(...)

```python
kwargs = dict(t_step_min=0.1, t_window='auto', verbose=True)
```

### Step 4: Assign pos = compute_chpi_amplitudes(...)

```python
pos = compute_chpi_amplitudes(raw, **kwargs)
```

### Step 5: Call raw.load_data()

```python
raw.load_data()
```

### Step 6: Assign pos_preload = compute_chpi_amplitudes(...)

```python
pos_preload = compute_chpi_amplitudes(raw, **kwargs)
```

**Verification:**
```python
assert object_diff(pos, pos_preload) == ''
```


## Complete Example

```python
# Workflow
'Test calculation of cHPI positions with and without data loaded.'
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes').crop(0, 2)
kwargs = dict(t_step_min=0.1, t_window='auto', verbose=True)
pos = compute_chpi_amplitudes(raw, **kwargs)
raw.load_data()
pos_preload = compute_chpi_amplitudes(raw, **kwargs)
assert object_diff(pos, pos_preload) == ''
```

## Next Steps


---

*Source: test_chpi.py:318 | Complexity: Intermediate | Last updated: 2026-05-18*