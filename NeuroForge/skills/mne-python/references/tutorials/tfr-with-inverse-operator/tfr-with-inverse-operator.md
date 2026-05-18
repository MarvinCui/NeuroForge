# How To: Tfr With Inverse Operator

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate Epochs: Test time freq with MNE inverse computation.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.minimum_norm.time_frequency`
- `mne.time_frequency.multitaper`

**Setup Required:**
```python
# Fixtures: method
```

## Step-by-Step Guide

### Step 1: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events3, event_id, tmin, tmax, picks=picks, baseline=(None, 0), reject=dict(grad=4e-10, eog=0.00015), preload=True)
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
epochs = Epochs(raw, events3, event_id, tmin, tmax, picks=picks, baseline=(None, 0), reject=dict(grad=4e-10, eog=0.00015), preload=True)
```

## Next Steps


---

*Source: test_time_frequency.py:59 | Complexity: Beginner | Last updated: 2026-05-18*