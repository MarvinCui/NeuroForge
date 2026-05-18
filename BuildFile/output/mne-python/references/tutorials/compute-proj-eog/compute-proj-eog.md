# How To: Compute Proj Eog

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate compute_proj_eog: Test computation of EOG SSP projectors.

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
# Fixtures: average, short_raw
```

## Step-by-Step Guide

### Step 1: Assign unknown = compute_proj_eog(...)

```python
projs, events = compute_proj_eog(raw, n_mag=2, n_grad=2, n_eeg=2, bads=['MEG 2443'], average=average, avg_ref=True, no_proj=False, l_freq=None, h_freq=None, reject=None, tmax=dur_use, filter_length=1000)
```


## Complete Example

```python
# Setup
# Fixtures: average, short_raw

# Workflow
projs, events = compute_proj_eog(raw, n_mag=2, n_grad=2, n_eeg=2, bads=['MEG 2443'], average=average, avg_ref=True, no_proj=False, l_freq=None, h_freq=None, reject=None, tmax=dur_use, filter_length=1000)
```

## Next Steps


---

*Source: test_ssp.py:109 | Complexity: Beginner | Last updated: 2026-05-18*