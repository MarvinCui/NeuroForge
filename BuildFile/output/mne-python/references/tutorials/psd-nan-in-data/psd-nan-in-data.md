# How To: Psd Nan In Data

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: psd_array_welch should fail if +Inf lies inside analyzed samples.

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

### Step 1: 'psd_array_welch should fail if +Inf lies inside analyzed samples.'

```python
'psd_array_welch should fail if +Inf lies inside analyzed samples.'
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
rng = np.random.RandomState(0)
```

### Step 4: Assign x = rng.standard_normal(...)

```python
x = rng.standard_normal(size=(2, n_samples))
```

### Step 5: Assign unknown = value

```python
x[0, 800] = np.inf
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
'psd_array_welch should fail if +Inf lies inside analyzed samples.'
n_samples, n_fft, n_overlap = (2048, 256, 128)
rng = np.random.RandomState(0)
x = rng.standard_normal(size=(2, n_samples))
x[0, 800] = np.inf
with pytest.warns(RuntimeWarning, match='Non-finite values'):
    psds, freqs = psd_array_welch(x, float(n_fft), n_fft=n_fft, n_overlap=n_overlap)
assert np.isnan(psds[0]).all()
assert np.isfinite(psds[1]).any()
```

## Next Steps


---

*Source: test_psd.py:231 | Complexity: Intermediate | Last updated: 2026-05-18*