# How To: Averaging Epochstfr

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that EpochsTFR averaging methods work.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test that EpochsTFR averaging methods work.'

```python
'Test that EpochsTFR averaging methods work.'
```

**Verification:**
```python
assert_array_equal(func(power.data, axis=0), avgpower.data)
```

### Step 2: Assign event_id = 1

```python
event_id = 1
```

**Verification:**
```python
assert repr(avgpower).startswith('<Average Power from Epochs')
```

### Step 3: Assign tmin = value

```python
tmin = -0.2
```

### Step 4: Assign tmax = 0.498

```python
tmax = 0.498
```

### Step 5: Assign freqs = np.arange(...)

```python
freqs = np.arange(6, 20, 5)
```

### Step 6: Assign n_cycles = value

```python
n_cycles = freqs / 4.0
```

### Step 7: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

### Step 8: Assign events = value

```python
events = read_events(event_fname)[:4]
```

### Step 9: Assign include = value

```python
include = []
```

### Step 10: Assign exclude = value

```python
exclude = raw.info['bads'] + ['MEG 2443', 'EEG 053']
```

### Step 11: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg='grad', eeg=False, stim=False, include=include, exclude=exclude)
```

### Step 12: Assign picks = value

```python
picks = picks[:2]
```

### Step 13: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks)
```

### Step 14: Assign power = tfr_morlet(...)

```python
power = tfr_morlet(epochs, freqs=freqs, n_cycles=n_cycles, average=False, use_fft=True, return_itc=False)
```

### Step 15: Assign tapered = epochs.compute_tfr(...)

```python
tapered = epochs.compute_tfr(method='multitaper', freqs=freqs, n_cycles=n_cycles, output='complex')
```

### Step 16: Assign avgpower = power.average(...)

```python
avgpower = power.average()
```

**Verification:**
```python
assert repr(avgpower).startswith('<Average Power from Epochs')
```

### Step 17: Assign avgpower = power.average(...)

```python
avgpower = power.average(method=method)
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(func(power.data, axis=0), avgpower.data)
```

### Step 19: Call power.average()

```python
power.average(method=np.mean)
```

### Step 20: Call tapered.average()

```python
tapered.average()
```


## Complete Example

```python
# Workflow
'Test that EpochsTFR averaging methods work.'
event_id = 1
tmin = -0.2
tmax = 0.498
freqs = np.arange(6, 20, 5)
n_cycles = freqs / 4.0
raw = read_raw_fif(raw_fname)
events = read_events(event_fname)[:4]
include = []
exclude = raw.info['bads'] + ['MEG 2443', 'EEG 053']
picks = pick_types(raw.info, meg='grad', eeg=False, stim=False, include=include, exclude=exclude)
picks = picks[:2]
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks)
power = tfr_morlet(epochs, freqs=freqs, n_cycles=n_cycles, average=False, use_fft=True, return_itc=False)
for func, method in zip([np.mean, np.median, np.mean], ['mean', 'median', lambda x: np.mean(x, axis=0)]):
    avgpower = power.average(method=method)
    assert_array_equal(func(power.data, axis=0), avgpower.data)
with pytest.raises(RuntimeError, match='EpochsTFR.average\\(\\) got .* shape \\(\\), but it should be'):
    power.average(method=np.mean)
tapered = epochs.compute_tfr(method='multitaper', freqs=freqs, n_cycles=n_cycles, output='complex')
with pytest.raises(NotImplementedError, match='Averaging multitaper tapers .* is not supported.'):
    tapered.average()
avgpower = power.average()
assert repr(avgpower).startswith('<Average Power from Epochs')
```

## Next Steps


---

*Source: test_tfr.py:1187 | Complexity: Advanced | Last updated: 2026-05-18*