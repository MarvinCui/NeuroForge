# How To: Psd Array Welch Nperseg Kwarg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test n_per_seg and padding in psd_array_welch().

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

### Step 1: 'Test n_per_seg and padding in psd_array_welch().'

```python
'Test n_per_seg and padding in psd_array_welch().'
```

**Verification:**
```python
assert len(freqs1) == np.floor(len(freqs2) / 2.0)
```

### Step 2: Assign unknown = _make_psd_data(...)

```python
data, sfreq, _ = _make_psd_data()
```

**Verification:**
```python
assert psds1.shape[-1] == np.floor(psds2.shape[-1] / 2.0)
```

### Step 3: Assign kwargs = dict(...)

```python
kwargs = dict(fmin=2, fmax=70, n_per_seg=128)
```

### Step 4: Assign unknown = psd_array_welch(...)

```python
psds1, freqs1 = psd_array_welch(data, sfreq, n_fft=128, **kwargs)
```

### Step 5: Assign unknown = psd_array_welch(...)

```python
psds2, freqs2 = psd_array_welch(data, sfreq, n_fft=256, **kwargs)
```

**Verification:**
```python
assert len(freqs1) == np.floor(len(freqs2) / 2.0)
```

### Step 6: Call kwargs.update()

```python
kwargs.update(n_per_seg=None)
```

### Step 7: Assign bad_n_fft = int(...)

```python
bad_n_fft = int(data.shape[-1] * 1.1)
```

### Step 8: Call psd_array_welch()

```python
psd_array_welch(data, sfreq, n_fft=bad_n_fft, **kwargs)
```

### Step 9: Call kwargs.update()

```python
kwargs.update(n_per_seg=64)
```

### Step 10: Call psd_array_welch()

```python
psd_array_welch(data, sfreq, n_fft=128, n_overlap=90, **kwargs)
```

### Step 11: Call psd_array_welch()

```python
psd_array_welch(data, sfreq, fmin=10, fmax=1)
```


## Complete Example

```python
# Workflow
'Test n_per_seg and padding in psd_array_welch().'
data, sfreq, _ = _make_psd_data()
kwargs = dict(fmin=2, fmax=70, n_per_seg=128)
psds1, freqs1 = psd_array_welch(data, sfreq, n_fft=128, **kwargs)
psds2, freqs2 = psd_array_welch(data, sfreq, n_fft=256, **kwargs)
assert len(freqs1) == np.floor(len(freqs2) / 2.0)
assert psds1.shape[-1] == np.floor(psds2.shape[-1] / 2.0)
with pytest.raises(ValueError, match='n_fft is not allowed to be > n_tim'):
    kwargs.update(n_per_seg=None)
    bad_n_fft = int(data.shape[-1] * 1.1)
    psd_array_welch(data, sfreq, n_fft=bad_n_fft, **kwargs)
with pytest.raises(ValueError, match='n_overlap cannot be greater'):
    kwargs.update(n_per_seg=64)
    psd_array_welch(data, sfreq, n_fft=128, n_overlap=90, **kwargs)
with pytest.raises(ValueError, match='No frequencies found'):
    psd_array_welch(data, sfreq, fmin=10, fmax=1)
```

## Next Steps


---

*Source: test_psd.py:105 | Complexity: Advanced | Last updated: 2026-05-18*