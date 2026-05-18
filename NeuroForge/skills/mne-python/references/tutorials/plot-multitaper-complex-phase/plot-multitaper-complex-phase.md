# How To: Plot Multitaper Complex Phase

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test TFR plotting of data with a taper dimension.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `re`
- `itertools`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.collections`
- `numpy.testing`
- `mne`
- `mne`
- `mne.epochs`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.tfr`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz.utils`
- `test_spectrum`
- `pandas.testing`

**Setup Required:**
```python
# Fixtures: output
```

## Step-by-Step Guide

### Step 1: 'Test TFR plotting of data with a taper dimension.'

```python
'Test TFR plotting of data with a taper dimension.'
```

### Step 2: Assign unknown = value

```python
n_chans, n_tapers, n_freqs, n_times = (3, 4, 2, 3)
```

### Step 3: Assign data = np.random.rand(...)

```python
data = np.random.rand(n_chans, n_tapers, n_freqs, n_times)
```

### Step 4: Assign times = np.arange(...)

```python
times = np.arange(n_times)
```

### Step 5: Assign freqs = np.arange(...)

```python
freqs = np.arange(n_freqs)
```

### Step 6: Assign weights = np.random.rand(...)

```python
weights = np.random.rand(n_tapers, n_freqs)
```

### Step 7: Assign info = mne.create_info(...)

```python
info = mne.create_info(n_chans, 1000.0, 'eeg')
```

### Step 8: Assign tfr = AverageTFRArray(...)

```python
tfr = AverageTFRArray(info=info, data=data, times=times, freqs=freqs, weights=weights)
```

### Step 9: Call tfr.plot()

```python
tfr.plot()
```

### Step 10: Assign data = value

```python
data = data + np.random.rand(*data.shape) * 1j
```


## Complete Example

```python
# Setup
# Fixtures: output

# Workflow
'Test TFR plotting of data with a taper dimension.'
n_chans, n_tapers, n_freqs, n_times = (3, 4, 2, 3)
data = np.random.rand(n_chans, n_tapers, n_freqs, n_times)
if output == 'complex':
    data = data + np.random.rand(*data.shape) * 1j
times = np.arange(n_times)
freqs = np.arange(n_freqs)
weights = np.random.rand(n_tapers, n_freqs)
info = mne.create_info(n_chans, 1000.0, 'eeg')
tfr = AverageTFRArray(info=info, data=data, times=times, freqs=freqs, weights=weights)
tfr.plot()
```

## Next Steps


---

*Source: test_tfr.py:891 | Complexity: Advanced | Last updated: 2026-05-18*