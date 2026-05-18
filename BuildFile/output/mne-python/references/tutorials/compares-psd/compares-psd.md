# How To: Compares Psd

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test PSD estimation on raw for plt.psd and scipy.signal.welch.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.signal`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.time_frequency.psd`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test PSD estimation on raw for plt.psd and scipy.signal.welch.'

```python
'Test PSD estimation on raw for plt.psd and scipy.signal.welch.'
```

**Verification:**
```python
assert_array_almost_equal(psds_mne, psds_scipy)
```

### Step 2: Assign unknown = _make_psd_data(...)

```python
data, sfreq, _ = _make_psd_data()
```

**Verification:**
```python
assert_array_equal(freqs_mne, freqs_scipy)
```

### Step 3: Assign n_fft = 2048

```python
n_fft = 2048
```

**Verification:**
```python
assert psds_mne.shape == (data.shape[0], len(freqs_mne))
```

### Step 4: Assign unknown = value

```python
fmin, fmax = (2, 70)
```

**Verification:**
```python
assert psds_scipy.shape == (data.shape[0], len(freqs_scipy))
```

### Step 5: Assign unknown = psd_array_welch(...)

```python
psds_mne, freqs_mne = psd_array_welch(data, sfreq, fmin=fmin, fmax=fmax, n_fft=n_fft)
```

**Verification:**
```python
assert np.sum(freqs_mne < 0) == 0
```

### Step 6: Assign unknown = welch(...)

```python
freqs_scipy, psds_scipy = welch(data, fs=sfreq, nperseg=n_fft, noverlap=0, window='hamming')
```

**Verification:**
```python
assert np.sum(freqs_scipy < 0) == 0
```

### Step 7: Assign mask = value

```python
mask = (freqs_scipy >= fmin) & (freqs_scipy <= fmax)
```

**Verification:**
```python
assert np.sum(psds_mne < 0) == 0
```

### Step 8: Assign freqs_scipy = value

```python
freqs_scipy = freqs_scipy[mask]
```

**Verification:**
```python
assert np.sum(psds_scipy < 0) == 0
```

### Step 9: Assign psds_scipy = value

```python
psds_scipy = psds_scipy[:, mask]
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(psds_mne, psds_scipy)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(freqs_mne, freqs_scipy)
```

**Verification:**
```python
assert psds_mne.shape == (data.shape[0], len(freqs_mne))
```


## Complete Example

```python
# Workflow
'Test PSD estimation on raw for plt.psd and scipy.signal.welch.'
data, sfreq, _ = _make_psd_data()
n_fft = 2048
fmin, fmax = (2, 70)
psds_mne, freqs_mne = psd_array_welch(data, sfreq, fmin=fmin, fmax=fmax, n_fft=n_fft)
freqs_scipy, psds_scipy = welch(data, fs=sfreq, nperseg=n_fft, noverlap=0, window='hamming')
mask = (freqs_scipy >= fmin) & (freqs_scipy <= fmax)
freqs_scipy = freqs_scipy[mask]
psds_scipy = psds_scipy[:, mask]
assert_array_almost_equal(psds_mne, psds_scipy)
assert_array_equal(freqs_mne, freqs_scipy)
assert psds_mne.shape == (data.shape[0], len(freqs_mne))
assert psds_scipy.shape == (data.shape[0], len(freqs_scipy))
assert np.sum(freqs_mne < 0) == 0
assert np.sum(freqs_scipy < 0) == 0
assert np.sum(psds_mne < 0) == 0
assert np.sum(psds_scipy < 0) == 0
```

## Next Steps


---

*Source: test_psd.py:196 | Complexity: Advanced | Last updated: 2026-05-18*