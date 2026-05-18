# How To: Averaging Freqsandtimes Epochstfr

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that EpochsTFR averaging freqs methods work.

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

### Step 1: 'Test that EpochsTFR averaging freqs methods work.'

```python
'Test that EpochsTFR averaging freqs methods work.'
```

**Verification:**
```python
assert_array_equal(avgpower.data, func(power.data, axis=2, keepdims=True))
```

### Step 2: Assign event_id = 1

```python
event_id = 1
```

**Verification:**
```python
assert_array_equal(avgpower.freqs, func(power.freqs, keepdims=True))
```

### Step 3: Assign tmin = value

```python
tmin = -0.2
```

**Verification:**
```python
assert isinstance(avgpower, EpochsTFR)
```

### Step 4: Assign tmax = 0.498

```python
tmax = 0.498
```

**Verification:**
```python
assert isinstance(avgpower, AverageTFR)
```

### Step 5: Assign freqs = np.arange(...)

```python
freqs = np.arange(6, 20, 5)
```

**Verification:**
```python
assert_array_equal(avgpower.data, func(power.data, axis=-1, keepdims=False))
```

### Step 6: Assign n_cycles = value

```python
n_cycles = freqs / 4.0
```

**Verification:**
```python
assert isinstance(avgpower, EpochsSpectrum)
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

### Step 15: Assign kwargs = dict(...)

```python
kwargs = dict(dim='freqs', copy=True)
```

### Step 16: Assign kwargs = dict(...)

```python
kwargs = dict(dim='times', copy=False)
```

### Step 17: Assign avgpower = power.average(...)

```python
avgpower = power.average(method=method, **kwargs)
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(avgpower.data, func(power.data, axis=2, keepdims=True))
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(avgpower.freqs, func(power.freqs, keepdims=True))
```

**Verification:**
```python
assert isinstance(avgpower, EpochsTFR)
```

### Step 20: Assign avgpower = avgpower.average(...)

```python
avgpower = avgpower.average()
```

**Verification:**
```python
assert isinstance(avgpower, AverageTFR)
```

### Step 21: Assign avgpower = power.average(...)

```python
avgpower = power.average(method=lambda x: np.mean(x, axis=3), **kwargs)
```

### Step 22: Assign avgpower = power.average(...)

```python
avgpower = power.average(method=method, **kwargs)
```

### Step 23: Call assert_array_equal()

```python
assert_array_equal(avgpower.data, func(power.data, axis=-1, keepdims=False))
```

**Verification:**
```python
assert isinstance(avgpower, EpochsSpectrum)
```

### Step 24: Assign avgpower = power.average(...)

```python
avgpower = power.average(method=lambda x: np.mean(x, axis=2), **kwargs)
```


## Complete Example

```python
# Workflow
'Test that EpochsTFR averaging freqs methods work.'
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
kwargs = dict(dim='freqs', copy=True)
for method, func in zip(('mean', 'median', lambda x: np.mean(x, axis=2)), (np.mean, np.median, np.mean)):
    avgpower = power.average(method=method, **kwargs)
    assert_array_equal(avgpower.data, func(power.data, axis=2, keepdims=True))
    assert_array_equal(avgpower.freqs, func(power.freqs, keepdims=True))
    assert isinstance(avgpower, EpochsTFR)
    avgpower = avgpower.average()
    assert isinstance(avgpower, AverageTFR)
with pytest.raises(RuntimeError, match='shape \\(1, 2, 3\\), but it should'):
    avgpower = power.average(method=lambda x: np.mean(x, axis=3), **kwargs)
kwargs = dict(dim='times', copy=False)
for method, func in zip(('mean', 'median', lambda x: np.mean(x, axis=3)), (np.mean, np.median, np.mean)):
    avgpower = power.average(method=method, **kwargs)
    assert_array_equal(avgpower.data, func(power.data, axis=-1, keepdims=False))
    assert isinstance(avgpower, EpochsSpectrum)
with pytest.raises(RuntimeError, match='shape \\(1, 2, 420\\), but it should'):
    avgpower = power.average(method=lambda x: np.mean(x, axis=2), **kwargs)
```

## Next Steps


---

*Source: test_tfr.py:1247 | Complexity: Advanced | Last updated: 2026-05-18*