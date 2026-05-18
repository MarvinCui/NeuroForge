# How To: Sorting

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test sorting learning during training.

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

### Step 1: 'Test sorting learning during training.'

```python
'Test sorting learning during training.'
```

**Verification:**
```python
assert any(sorter_tr != sorter_te)
```

### Step 2: Assign unknown = simulate_data(...)

```python
X, _, _ = simulate_data(n_trials=100, n_channels=20, n_samples=500)
```

**Verification:**
```python
assert all(sorter_in == sorter_out)
```

### Step 3: Assign X = np.reshape(...)

```python
X = np.reshape(X, (100, 20, 500))
```

### Step 4: Assign unknown = value

```python
Xtr, Xte = (X[:80], X[80:])
```

### Step 5: Assign sf = 250

```python
sf = 250
```

### Step 6: Assign n_channels = value

```python
n_channels = Xtr.shape[1]
```

### Step 7: Assign info = create_info(...)

```python
info = create_info(ch_names=n_channels, sfreq=sf, ch_types='eeg')
```

### Step 8: Assign filt_params_signal = dict(...)

```python
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
```

### Step 9: Assign filt_params_noise = dict(...)

```python
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
```

### Step 10: Assign ssd = SSD(...)

```python
ssd = SSD(info, filt_params_signal, filt_params_noise, n_components=None, sort_by_spectral_ratio=False)
```

### Step 11: Call ssd.fit()

```python
ssd.fit(Xtr)
```

### Step 12: Assign unknown = _get_spectral_ratio(...)

```python
_, sorter_tr = _get_spectral_ratio(ssd.transform(Xtr), ssd.sfreq_, ssd.n_fft_, ssd.freqs_signal_, ssd.freqs_noise_)
```

### Step 13: Assign unknown = _get_spectral_ratio(...)

```python
_, sorter_te = _get_spectral_ratio(ssd.transform(Xte), ssd.sfreq_, ssd.n_fft_, ssd.freqs_signal_, ssd.freqs_noise_)
```

**Verification:**
```python
assert any(sorter_tr != sorter_te)
```

### Step 14: Assign ssd = SSD(...)

```python
ssd = SSD(info, filt_params_signal, filt_params_noise, n_components=None, sort_by_spectral_ratio=True)
```

### Step 15: Call ssd.fit()

```python
ssd.fit(Xtr)
```

### Step 16: Assign sorter_in = value

```python
sorter_in = ssd.sorter_
```

### Step 17: Assign ssd = SSD(...)

```python
ssd = SSD(info, filt_params_signal, filt_params_noise, n_components=None, sort_by_spectral_ratio=False)
```

### Step 18: Call ssd.fit()

```python
ssd.fit(Xtr)
```

### Step 19: Assign unknown = _get_spectral_ratio(...)

```python
_, sorter_out = _get_spectral_ratio(ssd.transform(Xtr), ssd.sfreq_, ssd.n_fft_, ssd.freqs_signal_, ssd.freqs_noise_)
```

**Verification:**
```python
assert all(sorter_in == sorter_out)
```


## Complete Example

```python
# Workflow
'Test sorting learning during training.'
X, _, _ = simulate_data(n_trials=100, n_channels=20, n_samples=500)
X = np.reshape(X, (100, 20, 500))
Xtr, Xte = (X[:80], X[80:])
sf = 250
n_channels = Xtr.shape[1]
info = create_info(ch_names=n_channels, sfreq=sf, ch_types='eeg')
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
ssd = SSD(info, filt_params_signal, filt_params_noise, n_components=None, sort_by_spectral_ratio=False)
ssd.fit(Xtr)
_, sorter_tr = _get_spectral_ratio(ssd.transform(Xtr), ssd.sfreq_, ssd.n_fft_, ssd.freqs_signal_, ssd.freqs_noise_)
_, sorter_te = _get_spectral_ratio(ssd.transform(Xte), ssd.sfreq_, ssd.n_fft_, ssd.freqs_signal_, ssd.freqs_noise_)
assert any(sorter_tr != sorter_te)
ssd = SSD(info, filt_params_signal, filt_params_noise, n_components=None, sort_by_spectral_ratio=True)
ssd.fit(Xtr)
sorter_in = ssd.sorter_
ssd = SSD(info, filt_params_signal, filt_params_noise, n_components=None, sort_by_spectral_ratio=False)
ssd.fit(Xtr)
_, sorter_out = _get_spectral_ratio(ssd.transform(Xtr), ssd.sfreq_, ssd.n_fft_, ssd.freqs_signal_, ssd.freqs_noise_)
assert all(sorter_in == sorter_out)
```

## Next Steps


---

*Source: test_ssd.py:364 | Complexity: Advanced | Last updated: 2026-05-18*