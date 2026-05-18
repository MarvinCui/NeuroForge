# How To: Picks Arg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that picks argument works as expected.

## Prerequisites

**Required Modules:**
- `sys`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.pipeline`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne._fiff.pick`
- `mne.decoding`
- `mne.decoding._mod_ged`
- `mne.decoding.ssd`
- `mne.filter`
- `mne.time_frequency`


## Step-by-Step Guide

### Step 1: 'Test that picks argument works as expected.'

```python
'Test that picks argument works as expected.'
```

### Step 2: Assign raw = io.read_raw_fif(...)

```python
raw = io.read_raw_fif(raw_fname, preload=False)
```

### Step 3: Assign events = read_events(...)

```python
events = read_events(event_name)
```

### Step 4: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=True, eeg=True, stim=False, ecg=False, eog=False, exclude='bads')
```

### Step 5: Call raw.add_proj()

```python
raw.add_proj([], remove_existing=True)
```

### Step 6: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, -0.1, 1, picks=picks, baseline=(None, 0), preload=True, proj=False)
```

### Step 7: Assign X = epochs.get_data(...)

```python
X = epochs.get_data(copy=False)
```

### Step 8: Assign filt_params_signal = dict(...)

```python
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=3, h_trans_bandwidth=3)
```

### Step 9: Assign filt_params_noise = dict(...)

```python
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=3, h_trans_bandwidth=3)
```

### Step 10: Assign picks = value

```python
picks = ['eeg']
```

### Step 11: Assign info = value

```python
info = epochs.info
```

### Step 12: Assign picks_idx = _picks_to_idx(...)

```python
picks_idx = _picks_to_idx(info, picks)
```

### Step 13: Assign ssd = SSD(...)

```python
ssd = SSD(info, filt_params_signal, filt_params_noise, picks=picks_idx, return_filtered=False)
```

### Step 14: Call ssd.fit.transform()

```python
ssd.fit(X).transform(X)
```

### Step 15: Assign ssd = SSD(...)

```python
ssd = SSD(info, filt_params_signal, filt_params_noise, picks=picks_idx, return_filtered=True, n_fft=64)
```

### Step 16: Call ssd.fit.transform()

```python
ssd.fit(X).transform(X)
```


## Complete Example

```python
# Workflow
'Test that picks argument works as expected.'
raw = io.read_raw_fif(raw_fname, preload=False)
events = read_events(event_name)
picks = pick_types(raw.info, meg=True, eeg=True, stim=False, ecg=False, eog=False, exclude='bads')
raw.add_proj([], remove_existing=True)
epochs = Epochs(raw, events, event_id, -0.1, 1, picks=picks, baseline=(None, 0), preload=True, proj=False)
X = epochs.get_data(copy=False)
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=3, h_trans_bandwidth=3)
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=3, h_trans_bandwidth=3)
picks = ['eeg']
info = epochs.info
picks_idx = _picks_to_idx(info, picks)
ssd = SSD(info, filt_params_signal, filt_params_noise, picks=picks_idx, return_filtered=False)
ssd.fit(X).transform(X)
ssd = SSD(info, filt_params_signal, filt_params_noise, picks=picks_idx, return_filtered=True, n_fft=64)
ssd.fit(X).transform(X)
```

## Next Steps


---

*Source: test_ssd.py:515 | Complexity: Advanced | Last updated: 2026-05-18*