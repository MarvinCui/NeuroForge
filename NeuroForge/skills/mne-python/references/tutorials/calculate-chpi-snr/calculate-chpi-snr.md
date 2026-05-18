# How To: Calculate Chpi Snr

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test cHPI SNR calculation.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.interpolate`
- `scipy.spatial.distance`
- `mne`
- `mne._fiff.constants`
- `mne.chpi`
- `mne.datasets`
- `mne.forward._compute_forward`
- `mne.io`
- `mne.simulation`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz`
- `scipy.signal`


## Step-by-Step Guide

### Step 1: 'Test cHPI SNR calculation.'

```python
'Test cHPI SNR calculation.'
```

**Verification:**
```python
assert set(result) == keys.union({'times', 'freqs'})
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes')
```

**Verification:**
```python
assert_allclose(result['mag_snr'].shape[0], n_pts, atol=5)
```

### Step 3: Call raw.load_data()

```python
raw.load_data()
```

**Verification:**
```python
assert_allclose(result['mag_snr'][:n_nan], np.nan)
```

### Step 4: Assign unknown = value

```python
raw.info['bads'] = ['MEG0342', 'MEG1443']
```

**Verification:**
```python
assert result['mag_snr'][n_nan:].min() > 1
```

### Step 5: Assign stop = value

```python
stop = int(round(raw.info['sfreq'])) * 2
```

**Verification:**
```python
assert result['mag_snr'][n_nan:].max() < 40
```

### Step 6: Assign unknown = 0

```python
raw._data[raw.ch_names.index('STI201'), :stop] = 0
```

**Verification:**
```python
assert result['grad_snr'][n_nan:].min() > 1
```

### Step 7: Assign result = compute_chpi_snr(...)

```python
result = compute_chpi_snr(raw)
```

**Verification:**
```python
assert result['grad_snr'][n_nan:].max() < 40
```

### Step 8: Assign keys = value

```python
keys = {f'{ch_type}_{key}' for ch_type in ('mag', 'grad') for key in ('snr', 'power', 'resid')}
```

**Verification:**
```python
assert set(result) == keys.union({'times', 'freqs'})
```

### Step 9: Assign n_pts = value

```python
n_pts = len(raw.times) // int(round(raw.info['sfreq'] * 0.01))
```

### Step 10: Call assert_allclose()

```python
assert_allclose(result['mag_snr'].shape[0], n_pts, atol=5)
```

### Step 11: Assign n_nan = value

```python
n_nan = np.where(result['times'] <= raw.first_time + 2)[0][-1]
```

### Step 12: Call assert_allclose()

```python
assert_allclose(result['mag_snr'][:n_nan], np.nan)
```

**Verification:**
```python
assert result['mag_snr'][n_nan:].min() > 1
```


## Complete Example

```python
# Workflow
'Test cHPI SNR calculation.'
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes')
raw.load_data()
raw.info['bads'] = ['MEG0342', 'MEG1443']
stop = int(round(raw.info['sfreq'])) * 2
raw._data[raw.ch_names.index('STI201'), :stop] = 0
result = compute_chpi_snr(raw)
keys = {f'{ch_type}_{key}' for ch_type in ('mag', 'grad') for key in ('snr', 'power', 'resid')}
assert set(result) == keys.union({'times', 'freqs'})
n_pts = len(raw.times) // int(round(raw.info['sfreq'] * 0.01))
assert_allclose(result['mag_snr'].shape[0], n_pts, atol=5)
n_nan = np.where(result['times'] <= raw.first_time + 2)[0][-1]
assert_allclose(result['mag_snr'][:n_nan], np.nan)
assert result['mag_snr'][n_nan:].min() > 1
assert result['mag_snr'][n_nan:].max() < 40
assert result['grad_snr'][n_nan:].min() > 1
assert result['grad_snr'][n_nan:].max() < 40
```

## Next Steps


---

*Source: test_chpi.py:395 | Complexity: Advanced | Last updated: 2026-05-18*