# How To: Get Spectral Ratio

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that method is the same as function in _mod_ged.py.

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

### Step 1: 'Test that method is the same as function in _mod_ged.py.'

```python
'Test that method is the same as function in _mod_ged.py.'
```

**Verification:**
```python
assert_array_equal(spec_ratio_ssd, spec_ratio_ged)
```

### Step 2: Assign unknown = simulate_data(...)

```python
X, _, _ = simulate_data()
```

**Verification:**
```python
assert_array_equal(sorter_spec_ssd, sorter_spec_ged)
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
ssd = SSD(info, filt_params_signal, filt_params_noise, n_components=None, sort_by_spectral_ratio=False)
```

### Step 9: Call ssd.fit()

```python
ssd.fit(X)
```

### Step 10: Assign ssd_sources = ssd.transform(...)

```python
ssd_sources = ssd.transform(X)
```

### Step 11: Assign unknown = ssd.get_spectral_ratio(...)

```python
spec_ratio_ssd, sorter_spec_ssd = ssd.get_spectral_ratio(ssd_sources)
```

### Step 12: Assign unknown = _get_spectral_ratio(...)

```python
spec_ratio_ged, sorter_spec_ged = _get_spectral_ratio(ssd_sources, ssd.sfreq_, ssd.n_fft_, ssd.freqs_signal_, ssd.freqs_noise_)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(spec_ratio_ssd, spec_ratio_ged)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(sorter_spec_ssd, sorter_spec_ged)
```


## Complete Example

```python
# Workflow
'Test that method is the same as function in _mod_ged.py.'
X, _, _ = simulate_data()
sf = 250
n_channels = X.shape[0]
info = create_info(ch_names=n_channels, sfreq=sf, ch_types='eeg')
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=1, h_trans_bandwidth=1)
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=1, h_trans_bandwidth=1)
ssd = SSD(info, filt_params_signal, filt_params_noise, n_components=None, sort_by_spectral_ratio=False)
ssd.fit(X)
ssd_sources = ssd.transform(X)
spec_ratio_ssd, sorter_spec_ssd = ssd.get_spectral_ratio(ssd_sources)
spec_ratio_ged, sorter_spec_ged = _get_spectral_ratio(ssd_sources, ssd.sfreq_, ssd.n_fft_, ssd.freqs_signal_, ssd.freqs_noise_)
assert_array_equal(spec_ratio_ssd, spec_ratio_ged)
assert_array_equal(sorter_spec_ssd, sorter_spec_ged)
```

## Next Steps


---

*Source: test_ssd.py:641 | Complexity: Advanced | Last updated: 2026-05-18*