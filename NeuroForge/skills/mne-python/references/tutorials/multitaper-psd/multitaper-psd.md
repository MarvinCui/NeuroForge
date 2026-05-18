# How To: Multitaper Psd

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test multi-taper PSD computation.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: n_times, adaptive, n_jobs
```

## Step-by-Step Guide

### Step 1: 'Test multi-taper PSD computation.'

```python
'Test multi-taper PSD computation.'
```

**Verification:**
```python
assert_array_almost_equal(psd, psd_ni, decimal=4)
```

### Step 2: Assign ni = pytest.importorskip(...)

```python
ni = pytest.importorskip('nitime')
```

### Step 3: Assign n_channels = 5

```python
n_channels = 5
```

### Step 4: Assign data = np.random.default_rng.random(...)

```python
data = np.random.default_rng(0).random((n_channels, n_times))
```

### Step 5: Assign sfreq = 500

```python
sfreq = 500
```

### Step 6: Assign unknown = psd_array_multitaper(...)

```python
psd, freqs = psd_array_multitaper(data, sfreq, adaptive=adaptive, n_jobs=n_jobs, normalization='full')
```

### Step 7: Assign unknown = ni.algorithms.spectral.multi_taper_psd(...)

```python
freqs_ni, psd_ni, _ = ni.algorithms.spectral.multi_taper_psd(data, sfreq, adaptive=adaptive, jackknife=False)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(psd, psd_ni, decimal=4)
```

### Step 9: Call psd_array_multitaper()

```python
psd_array_multitaper(data, sfreq, normalization='foo')
```

### Step 10: Call psd_array_multitaper()

```python
psd_array_multitaper(data, sfreq, bandwidth=4.9)
```


## Complete Example

```python
# Setup
# Fixtures: n_times, adaptive, n_jobs

# Workflow
'Test multi-taper PSD computation.'
ni = pytest.importorskip('nitime')
n_channels = 5
data = np.random.default_rng(0).random((n_channels, n_times))
sfreq = 500
with pytest.raises(ValueError, match="Invalid value for the 'normaliza"):
    psd_array_multitaper(data, sfreq, normalization='foo')
psd, freqs = psd_array_multitaper(data, sfreq, adaptive=adaptive, n_jobs=n_jobs, normalization='full')
freqs_ni, psd_ni, _ = ni.algorithms.spectral.multi_taper_psd(data, sfreq, adaptive=adaptive, jackknife=False)
assert_array_almost_equal(psd, psd_ni, decimal=4)
del freqs, freqs_ni
with pytest.raises(ValueError, match='use a value of at least'):
    psd_array_multitaper(data, sfreq, bandwidth=4.9)
```

## Next Steps


---

*Source: test_multitaper.py:39 | Complexity: Advanced | Last updated: 2026-05-18*