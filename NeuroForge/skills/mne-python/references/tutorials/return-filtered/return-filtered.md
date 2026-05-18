# How To: Return Filtered

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test return filtered option.

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

### Step 1: 'Test return filtered option.'

```python
'Test return filtered option.'
```

**Verification:**
```python
assert freqs_up == freqs_sig
```

### Step 2: Assign unknown = simulate_data(...)

```python
X, _, _ = simulate_data(SNR=0.9, freqs_sig=[4, 13])
```

**Verification:**
```python
assert freqs_up != freqs_sig
```

### Step 3: Assign sf = 250

```python
sf = 250
```

### Step 4: Assign n_channels = value

```python
n_channels = X.shape[0]
```

### Step 5: Assign info = create_info(...)

```python
info = create_info(ch_names=n_channels, sfreq=sf, ch_types='eeg')
```

### Step 6: Assign filt_params_signal = dict(...)

```python
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=1, h_trans_bandwidth=1)
```

### Step 7: Assign filt_params_noise = dict(...)

```python
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=1, h_trans_bandwidth=1)
```

### Step 8: Assign ssd = SSD(...)

```python
ssd = SSD(info, filt_params_signal, filt_params_noise, sort_by_spectral_ratio=False, return_filtered=True)
```

### Step 9: Call ssd.fit()

```python
ssd.fit(X)
```

### Step 10: Assign out = ssd.transform(...)

```python
out = ssd.transform(X)
```

### Step 11: Assign unknown = psd_array_welch(...)

```python
psd_out, freqs = psd_array_welch(out[0], sfreq=250, n_fft=250)
```

### Step 12: Assign freqs_up = value

```python
freqs_up = (int(freqs[psd_out > 0.5][0]), int(freqs[psd_out > 0.5][-1]))
```

**Verification:**
```python
assert freqs_up == freqs_sig
```

### Step 13: Assign ssd = SSD(...)

```python
ssd = SSD(info, filt_params_signal, filt_params_noise, sort_by_spectral_ratio=False, return_filtered=False)
```

### Step 14: Call ssd.fit()

```python
ssd.fit(X)
```

### Step 15: Assign out = ssd.transform(...)

```python
out = ssd.transform(X)
```

### Step 16: Assign unknown = psd_array_welch(...)

```python
psd_out, freqs = psd_array_welch(out[0], sfreq=250, n_fft=250)
```

### Step 17: Assign freqs_up = value

```python
freqs_up = (int(freqs[psd_out > 0.5][0]), int(freqs[psd_out > 0.5][-1]))
```

**Verification:**
```python
assert freqs_up != freqs_sig
```


## Complete Example

```python
# Workflow
'Test return filtered option.'
X, _, _ = simulate_data(SNR=0.9, freqs_sig=[4, 13])
sf = 250
n_channels = X.shape[0]
info = create_info(ch_names=n_channels, sfreq=sf, ch_types='eeg')
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=1, h_trans_bandwidth=1)
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=1, h_trans_bandwidth=1)
ssd = SSD(info, filt_params_signal, filt_params_noise, sort_by_spectral_ratio=False, return_filtered=True)
ssd.fit(X)
out = ssd.transform(X)
psd_out, freqs = psd_array_welch(out[0], sfreq=250, n_fft=250)
freqs_up = (int(freqs[psd_out > 0.5][0]), int(freqs[psd_out > 0.5][-1]))
assert freqs_up == freqs_sig
ssd = SSD(info, filt_params_signal, filt_params_noise, sort_by_spectral_ratio=False, return_filtered=False)
ssd.fit(X)
out = ssd.transform(X)
psd_out, freqs = psd_array_welch(out[0], sfreq=250, n_fft=250)
freqs_up = (int(freqs[psd_out > 0.5][0]), int(freqs[psd_out > 0.5][-1]))
assert freqs_up != freqs_sig
```

## Next Steps


---

*Source: test_ssd.py:432 | Complexity: Advanced | Last updated: 2026-05-18*