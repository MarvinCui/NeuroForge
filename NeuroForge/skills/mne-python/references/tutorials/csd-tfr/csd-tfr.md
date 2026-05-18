# How To: Csd Tfr

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test computing cross-spectral density on time-frequency epochs.

## Prerequisites

**Required Modules:**
- `pickle`
- `itertools`
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `pytest`
- `mne`
- `mne.channels`
- `mne.proj`
- `mne.time_frequency`
- `mne.time_frequency.csd`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test computing cross-spectral density on time-frequency epochs.'

```python
'Test computing cross-spectral density on time-frequency epochs.'
```

**Verification:**
```python
assert_allclose(csd._data, csd_test._data)
```

### Step 2: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(11)
```

**Verification:**
```python
assert_array_equal(csd.frequencies, freqs)
```

### Step 3: Assign n_epochs = 6

```python
n_epochs = 6
```

### Step 4: Assign info = mne.io.read_info(...)

```python
info = mne.io.read_info(raw_fname)
```

### Step 5: Assign info = mne.pick_info(...)

```python
info = mne.pick_info(info, mne.pick_types(info, eeg=True))
```

### Step 6: Assign freqs = np.arange(...)

```python
freqs = np.arange(38, 40)
```

### Step 7: Assign times = np.linspace(...)

```python
times = np.linspace(0, 1, int(round(info['sfreq'])))
```

### Step 8: Assign data = value

```python
data = rng.normal(size=(n_epochs, len(info.ch_names), times.size)) * 1e-06
```

### Step 9: Assign epochs = mne.EpochsArray(...)

```python
epochs = mne.EpochsArray(data, info)
```

### Step 10: Assign csd_test = csd_morlet(...)

```python
csd_test = csd_morlet(epochs, freqs, n_cycles=7, tmin=0.25, tmax=0.75)
```

### Step 11: Assign epochs_tfr = tfr_morlet(...)

```python
epochs_tfr = tfr_morlet(epochs, freqs, n_cycles=7, average=False, return_itc=False, output='complex')
```

### Step 12: Assign csd = csd_tfr(...)

```python
csd = csd_tfr(epochs_tfr, tmin=0.25, tmax=0.75)
```

### Step 13: Call assert_allclose()

```python
assert_allclose(csd._data, csd_test._data)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(csd.frequencies, freqs)
```


## Complete Example

```python
# Workflow
'Test computing cross-spectral density on time-frequency epochs.'
rng = np.random.default_rng(11)
n_epochs = 6
info = mne.io.read_info(raw_fname)
info = mne.pick_info(info, mne.pick_types(info, eeg=True))
freqs = np.arange(38, 40)
times = np.linspace(0, 1, int(round(info['sfreq'])))
data = rng.normal(size=(n_epochs, len(info.ch_names), times.size)) * 1e-06
epochs = mne.EpochsArray(data, info)
csd_test = csd_morlet(epochs, freqs, n_cycles=7, tmin=0.25, tmax=0.75)
epochs_tfr = tfr_morlet(epochs, freqs, n_cycles=7, average=False, return_itc=False, output='complex')
csd = csd_tfr(epochs_tfr, tmin=0.25, tmax=0.75)
assert_allclose(csd._data, csd_test._data)
assert_array_equal(csd.frequencies, freqs)
```

## Next Steps


---

*Source: test_csd.py:634 | Complexity: Advanced | Last updated: 2026-05-18*