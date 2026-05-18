# How To: Psd Misaligned Nan Across Channels

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: If NaNs are present but masks are NOT aligned across channels.

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

### Step 1: 'If NaNs are present but masks are NOT aligned across channels.'

```python
'If NaNs are present but masks are NOT aligned across channels.'
```

**Verification:**
```python
assert np.isnan(psds[0]).all()
```

### Step 2: Assign unknown = value

```python
n_samples, n_fft, n_overlap = (2048, 256, 128)
```

**Verification:**
```python
assert np.isfinite(psds[1]).any()
```

### Step 3: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(42)
```

### Step 4: Assign x = rng.standard_normal(...)

```python
x = rng.standard_normal(size=(2, n_samples))
```

### Step 5: Assign unknown = value

```python
x[0, 500] = np.nan
```

**Verification:**
```python
assert np.isnan(psds[0]).all()
```

### Step 6: Assign unknown = psd_array_welch(...)

```python
psds, freqs = psd_array_welch(x, float(n_fft), n_fft=n_fft, n_overlap=n_overlap)
```


## Complete Example

```python
# Workflow
'If NaNs are present but masks are NOT aligned across channels.'
n_samples, n_fft, n_overlap = (2048, 256, 128)
rng = np.random.RandomState(42)
x = rng.standard_normal(size=(2, n_samples))
x[0, 500] = np.nan
with pytest.warns(RuntimeWarning, match='Non-finite values'):
    psds, freqs = psd_array_welch(x, float(n_fft), n_fft=n_fft, n_overlap=n_overlap)
assert np.isnan(psds[0]).all()
assert np.isfinite(psds[1]).any()
```

## Next Steps


---

*Source: test_psd.py:248 | Complexity: Intermediate | Last updated: 2026-05-18*