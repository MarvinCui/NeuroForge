# How To: Compute Proj Ecg

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate compute_proj_ecg: Test computation of ECG SSP projectors.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.proj`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing.ssp`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: short_raw, average
```

## Step-by-Step Guide

### Step 1: Assign unknown = compute_proj_ecg(...)

```python
projs, events, drop_log = compute_proj_ecg(raw, n_mag=2, n_grad=2, n_eeg=2, ch_name='MEG 1531', bads=[], average=average, avg_ref=True, no_proj=True, l_freq=None, h_freq=None, tmax=dur_use, return_drop_log=True, qrs_threshold=1e-15)
```


## Complete Example

```python
# Setup
# Fixtures: short_raw, average

# Workflow
projs, events, drop_log = compute_proj_ecg(raw, n_mag=2, n_grad=2, n_eeg=2, ch_name='MEG 1531', bads=[], average=average, avg_ref=True, no_proj=True, l_freq=None, h_freq=None, tmax=dur_use, return_drop_log=True, qrs_threshold=1e-15)
```

## Next Steps


---

*Source: test_ssp.py:79 | Complexity: Beginner | Last updated: 2026-05-18*