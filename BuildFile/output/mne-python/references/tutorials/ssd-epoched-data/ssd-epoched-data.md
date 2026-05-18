# How To: Ssd Epoched Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Common Spatial Patterns algorithm on epoched data.

Compare the outputs when raw data is used.

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

### Step 1: 'Test Common Spatial Patterns algorithm on epoched data.\n\n    Compare the outputs when raw data is used.\n    '

```python
'Test Common Spatial Patterns algorithm on epoched data.\n\n    Compare the outputs when raw data is used.\n    '
```

**Verification:**
```python
assert_array_equal(sorter_spec_e[:n_components_true], sorter_spec[:n_components_true])
```

### Step 2: Assign unknown = simulate_data(...)

```python
X, A, S = simulate_data(n_trials=100, n_channels=20, n_samples=500)
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

### Step 6: Assign n_components_true = 5

```python
n_components_true = 5
```

### Step 7: Assign X_e = np.reshape(...)

```python
X_e = np.reshape(X, (100, 20, 500))
```

### Step 8: Assign filt_params_signal = dict(...)

```python
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
```

### Step 9: Assign filt_params_noise = dict(...)

```python
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
```

### Step 10: Assign ssd_e = SSD(...)

```python
ssd_e = SSD(info, filt_params_signal, filt_params_noise)
```

### Step 11: Call ssd_e.fit()

```python
ssd_e.fit(X_e)
```

### Step 12: Assign ssd = SSD(...)

```python
ssd = SSD(info, filt_params_signal, filt_params_noise)
```

### Step 13: Call ssd.fit()

```python
ssd.fit(X)
```

### Step 14: Assign unknown = _get_spectral_ratio(...)

```python
_, sorter_spec_e = _get_spectral_ratio(ssd_e.transform(X_e), ssd_e.sfreq_, ssd_e.n_fft_, ssd_e.freqs_signal_, ssd_e.freqs_noise_)
```

### Step 15: Assign unknown = _get_spectral_ratio(...)

```python
_, sorter_spec = _get_spectral_ratio(ssd.transform(X), ssd.sfreq_, ssd.n_fft_, ssd.freqs_signal_, ssd.freqs_noise_)
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(sorter_spec_e[:n_components_true], sorter_spec[:n_components_true])
```


## Complete Example

```python
# Workflow
'Test Common Spatial Patterns algorithm on epoched data.\n\n    Compare the outputs when raw data is used.\n    '
X, A, S = simulate_data(n_trials=100, n_channels=20, n_samples=500)
sf = 250
n_channels = X.shape[0]
info = create_info(ch_names=n_channels, sfreq=sf, ch_types='eeg')
n_components_true = 5
X_e = np.reshape(X, (100, 20, 500))
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
ssd_e = SSD(info, filt_params_signal, filt_params_noise)
ssd_e.fit(X_e)
ssd = SSD(info, filt_params_signal, filt_params_noise)
ssd.fit(X)
_, sorter_spec_e = _get_spectral_ratio(ssd_e.transform(X_e), ssd_e.sfreq_, ssd_e.n_fft_, ssd_e.freqs_signal_, ssd_e.freqs_noise_)
_, sorter_spec = _get_spectral_ratio(ssd.transform(X), ssd.sfreq_, ssd.n_fft_, ssd.freqs_signal_, ssd.freqs_noise_)
assert_array_equal(sorter_spec_e[:n_components_true], sorter_spec[:n_components_true])
```

## Next Steps


---

*Source: test_ssd.py:279 | Complexity: Advanced | Last updated: 2026-05-18*