# How To: Source Psd

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test source PSD computation from raw.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.minimum_norm.time_frequency`
- `mne.time_frequency.multitaper`

**Setup Required:**
```python
# Fixtures: method, pick_ori, pca
```

## Step-by-Step Guide

### Step 1: 'Test source PSD computation from raw.'

```python
'Test source PSD computation from raw.'
```

**Verification:**
```python
assert inverse_operator['source_ori'] == FIFF.FIFFV_MNE_FREE_ORI
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_data)
```

**Verification:**
```python
assert ev.data.shape == (len(ev.info['ch_names']), len(stc.times))
```

### Step 3: Call raw.crop.load_data()

```python
raw.crop(0, 5).load_data()
```

**Verification:**
```python
assert ev.times[0] >= fmin
```

### Step 4: Assign inverse_operator = read_inverse_operator(...)

```python
inverse_operator = read_inverse_operator(fname_inv)
```

**Verification:**
```python
assert ev.times[-1] <= fmax
```

### Step 5: Assign unknown = value

```python
fmin, fmax = (40, 65)
```

**Verification:**
```python
assert 58 <= ev.times[np.argmax(np.sum(ev.data, axis=0))] <= 61
```

### Step 6: Assign n_fft = 512

```python
n_fft = 512
```

**Verification:**
```python
assert ev.nave == 2
```

### Step 7: Assign unknown = compute_source_psd(...)

```python
stc, ev = compute_source_psd(raw, inverse_operator, lambda2=1.0 / 9.0, method=method, fmin=fmin, fmax=fmax, pick_ori=pick_ori, n_fft=n_fft, overlap=0.0, return_sensor=True, pca=pca, dB=True)
```

**Verification:**
```python
assert stc.shape[0] == inverse_operator['nsource']
```

### Step 8: Assign stc_dspm = stc

```python
stc_dspm = stc
```

**Verification:**
```python
assert stc.times[0] >= fmin
```

### Step 9: Assign unknown = compute_source_psd(...)

```python
stc_mne, _ = compute_source_psd(raw, inverse_operator, lambda2=1.0 / 9.0, method='MNE', fmin=fmin, fmax=fmax, pick_ori=pick_ori, n_fft=n_fft, overlap=0.0, return_sensor=True, dB=True)
```

**Verification:**
```python
assert stc.times[-1] <= fmax
```

### Step 10: Assign stc_dspm.data = value

```python
stc_dspm.data = 10 ** (stc_dspm.data / 10.0)
```

**Verification:**
```python
assert 58 <= stc.times[np.argmax(np.sum(stc.data, axis=0))] <= 61
```

### Step 11: Assign stc_mne.data = value

```python
stc_mne.data = 10 ** (stc_mne.data / 10.0)
```

**Verification:**
```python
assert_allclose(stc_dspm.data, stc_mne.data, atol=0.0001)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(stc_dspm.data, stc_mne.data, atol=0.0001)
```


## Complete Example

```python
# Setup
# Fixtures: method, pick_ori, pca

# Workflow
'Test source PSD computation from raw.'
raw = read_raw_fif(fname_data)
raw.crop(0, 5).load_data()
inverse_operator = read_inverse_operator(fname_inv)
fmin, fmax = (40, 65)
n_fft = 512
assert inverse_operator['source_ori'] == FIFF.FIFFV_MNE_FREE_ORI
stc, ev = compute_source_psd(raw, inverse_operator, lambda2=1.0 / 9.0, method=method, fmin=fmin, fmax=fmax, pick_ori=pick_ori, n_fft=n_fft, overlap=0.0, return_sensor=True, pca=pca, dB=True)
assert ev.data.shape == (len(ev.info['ch_names']), len(stc.times))
assert ev.times[0] >= fmin
assert ev.times[-1] <= fmax
assert 58 <= ev.times[np.argmax(np.sum(ev.data, axis=0))] <= 61
assert ev.nave == 2
assert stc.shape[0] == inverse_operator['nsource']
assert stc.times[0] >= fmin
assert stc.times[-1] <= fmax
assert 58 <= stc.times[np.argmax(np.sum(stc.data, axis=0))] <= 61
if method in ('sLORETA', 'dSPM'):
    stc_dspm = stc
    stc_mne, _ = compute_source_psd(raw, inverse_operator, lambda2=1.0 / 9.0, method='MNE', fmin=fmin, fmax=fmax, pick_ori=pick_ori, n_fft=n_fft, overlap=0.0, return_sensor=True, dB=True)
    stc_dspm.data = 10 ** (stc_dspm.data / 10.0)
    stc_dspm /= stc_dspm.mean()
    stc_mne.data = 10 ** (stc_mne.data / 10.0)
    stc_mne /= stc_mne.mean()
    assert_allclose(stc_dspm.data, stc_mne.data, atol=0.0001)
```

## Next Steps


---

*Source: test_time_frequency.py:279 | Complexity: Advanced | Last updated: 2026-05-18*