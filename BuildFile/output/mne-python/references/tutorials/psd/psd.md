# How To: Psd

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests the welch and multitaper PSD.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.signal`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.time_frequency.psd`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: psd_func, psd_kwargs
```

## Step-by-Step Guide

### Step 1: 'Tests the welch and multitaper PSD.'

```python
'Tests the welch and multitaper PSD.'
```

**Verification:**
```python
assert f'{n_fft}-point FFT on {n_fft} samples with 0 overl' in log
```

### Step 2: Assign unknown = _make_psd_data(...)

```python
data, sfreq, sinusoid_freqs = _make_psd_data()
```

**Verification:**
```python
assert 'hann window' in log
```

### Step 3: Call psd_kwargs.update()

```python
psd_kwargs.update(dict(fmin=2, fmax=70, verbose='debug'))
```

**Verification:**
```python
assert psds.shape == (data.shape[0], len(freqs))
```

### Step 4: Assign ixs_max = np.argmax(...)

```python
ixs_max = np.argmax(psds, axis=1)
```

**Verification:**
```python
assert np.sum(freqs < 0) == 0
```

### Step 5: Assign unknown = psd_func(...)

```python
psds, freqs = psd_func(data, sfreq, **psd_kwargs)
```

**Verification:**
```python
assert np.sum(psds < 0) == 0
```

### Step 6: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert np.abs(ixmax - ixtrue) < 2
```

### Step 7: Assign n_fft = value

```python
n_fft = psd_kwargs['n_fft']
```

**Verification:**
```python
assert f'{n_fft}-point FFT on {n_fft} samples with 0 overl' in log
```

### Step 8: Assign ixtrue = np.argmin(...)

```python
ixtrue = np.argmin(np.abs(ifreq - freqs))
```

**Verification:**
```python
assert np.abs(ixmax - ixtrue) < 2
```


## Complete Example

```python
# Setup
# Fixtures: psd_func, psd_kwargs

# Workflow
'Tests the welch and multitaper PSD.'
data, sfreq, sinusoid_freqs = _make_psd_data()
psd_kwargs.update(dict(fmin=2, fmax=70, verbose='debug'))
with catch_logging() as log:
    psds, freqs = psd_func(data, sfreq, **psd_kwargs)
if psd_func is psd_array_welch:
    log = log.getvalue()
    n_fft = psd_kwargs['n_fft']
    assert f'{n_fft}-point FFT on {n_fft} samples with 0 overl' in log
    assert 'hann window' in log
assert psds.shape == (data.shape[0], len(freqs))
assert np.sum(freqs < 0) == 0
assert np.sum(psds < 0) == 0
ixs_max = np.argmax(psds, axis=1)
for ixmax, ifreq in zip(ixs_max, sinusoid_freqs):
    ixtrue = np.argmin(np.abs(ifreq - freqs))
    assert np.abs(ixmax - ixtrue) < 2
```

## Next Steps


---

*Source: test_psd.py:81 | Complexity: Advanced | Last updated: 2026-05-18*