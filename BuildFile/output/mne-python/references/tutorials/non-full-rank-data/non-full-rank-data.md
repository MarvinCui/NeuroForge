# How To: Non Full Rank Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that the method works with non-full rank data.

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

### Step 1: 'Test that the method works with non-full rank data.'

```python
'Test that the method works with non-full rank data.'
```

**Verification:**
```python
assert np.linalg.matrix_rank(X) == rank
```

### Step 2: Assign n_channels = 10

```python
n_channels = 10
```

### Step 3: Assign unknown = simulate_data(...)

```python
X, _, _ = simulate_data(SNR=0.9, freqs_sig=[4, 13], n_channels=n_channels)
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(ch_names=n_channels, sfreq=250, ch_types='eeg')
```

### Step 5: Assign filt_params_signal = dict(...)

```python
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=1, h_trans_bandwidth=1)
```

### Step 6: Assign filt_params_noise = dict(...)

```python
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=1, h_trans_bandwidth=1)
```

### Step 7: Assign rank = 5

```python
rank = 5
```

### Step 8: Assign unknown = value

```python
X[rank:] = X[:rank]
```

**Verification:**
```python
assert np.linalg.matrix_rank(X) == rank
```

### Step 9: Assign ssd = SSD(...)

```python
ssd = SSD(info, filt_params_signal, filt_params_noise)
```

### Step 10: Call ssd.fit()

```python
ssd.fit(X)
```

### Step 11: Call pytest.xfail()

```python
pytest.xfail('Unknown linalg bug (Accelerate?)')
```


## Complete Example

```python
# Workflow
'Test that the method works with non-full rank data.'
n_channels = 10
X, _, _ = simulate_data(SNR=0.9, freqs_sig=[4, 13], n_channels=n_channels)
info = create_info(ch_names=n_channels, sfreq=250, ch_types='eeg')
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=1, h_trans_bandwidth=1)
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=1, h_trans_bandwidth=1)
rank = 5
X[rank:] = X[:rank]
assert np.linalg.matrix_rank(X) == rank
ssd = SSD(info, filt_params_signal, filt_params_noise)
if sys.platform == 'darwin':
    pytest.xfail('Unknown linalg bug (Accelerate?)')
ssd.fit(X)
```

## Next Steps


---

*Source: test_ssd.py:485 | Complexity: Advanced | Last updated: 2026-05-18*