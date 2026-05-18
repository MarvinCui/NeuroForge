# How To: Stockwell St No Zero Pad

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test stockwell power itc.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency._stockwell`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test stockwell power itc.'

```python
'Test stockwell power itc.'
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((20, 128))
```

### Step 3: Assign start_f = 1

```python
start_f = 1
```

### Step 4: Assign stop_f = 10

```python
stop_f = 10
```

### Step 5: Assign sfreq = 30

```python
sfreq = 30
```

### Step 6: Assign width = 2

```python
width = 2
```

### Step 7: Assign W = _precompute_st_windows(...)

```python
W = _precompute_st_windows(data.shape[-1], start_f, stop_f, sfreq, width)
```

### Step 8: Call _st_power_itc()

```python
_st_power_itc(data, 10, True, 0, 1, W)
```


## Complete Example

```python
# Workflow
'Test stockwell power itc.'
data = np.zeros((20, 128))
start_f = 1
stop_f = 10
sfreq = 30
width = 2
W = _precompute_st_windows(data.shape[-1], start_f, stop_f, sfreq, width)
_st_power_itc(data, 10, True, 0, 1, W)
```

## Next Steps


---

*Source: test_stockwell.py:59 | Complexity: Advanced | Last updated: 2026-05-18*