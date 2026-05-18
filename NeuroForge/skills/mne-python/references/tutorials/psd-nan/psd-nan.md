# How To: Psd Nan

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test handling of NaN in psd_array_welch.

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

### Step 1: 'Test handling of NaN in psd_array_welch.'

```python
'Test handling of NaN in psd_array_welch.'
```

**Verification:**
```python
assert_allclose(freqs, freqs_2)
```

### Step 2: Assign unknown = value

```python
n_samples, n_fft, n_overlap = (2048, 1024, 512)
```

**Verification:**
```python
assert_allclose(psds, psds_2)
```

### Step 3: Assign x = np.random.RandomState.randn(...)

```python
x = np.random.RandomState(0).randn(1, n_samples)
```

**Verification:**
```python
assert_allclose(freqs, freqs_2)
```

### Step 4: Assign unknown = psd_array_welch(...)

```python
psds, freqs = psd_array_welch(x[:, :n_fft + n_overlap], float(n_fft), n_fft=n_fft, n_overlap=n_overlap)
```

**Verification:**
```python
assert_allclose(psds[0], psds_2)
```

### Step 5: Assign unknown = value

```python
x[:, n_fft + n_overlap:] = np.nan
```

**Verification:**
```python
assert 'using 256-point FFT on 256 samples with 0 overlap' in log
```

### Step 6: Assign unknown = psd_array_welch(...)

```python
psds_2, freqs_2 = psd_array_welch(x, float(n_fft), n_fft=n_fft, n_overlap=n_overlap)
```

**Verification:**
```python
assert 'hamming window' in log
```

### Step 7: Call assert_allclose()

```python
assert_allclose(freqs, freqs_2)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(psds, psds_2)
```

### Step 9: Assign unknown = psd_array_welch(...)

```python
psds_2, freqs_2 = psd_array_welch(x[0], float(n_fft), n_fft=n_fft, n_overlap=n_overlap)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(freqs, freqs_2)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(psds[0], psds_2)
```

### Step 12: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'using 256-point FFT on 256 samples with 0 overlap' in log
```

### Step 13: Call psd_array_welch()

```python
psd_array_welch(x, float(n_fft), verbose='debug')
```


## Complete Example

```python
# Workflow
'Test handling of NaN in psd_array_welch.'
n_samples, n_fft, n_overlap = (2048, 1024, 512)
x = np.random.RandomState(0).randn(1, n_samples)
psds, freqs = psd_array_welch(x[:, :n_fft + n_overlap], float(n_fft), n_fft=n_fft, n_overlap=n_overlap)
x[:, n_fft + n_overlap:] = np.nan
psds_2, freqs_2 = psd_array_welch(x, float(n_fft), n_fft=n_fft, n_overlap=n_overlap)
assert_allclose(freqs, freqs_2)
assert_allclose(psds, psds_2)
psds_2, freqs_2 = psd_array_welch(x[0], float(n_fft), n_fft=n_fft, n_overlap=n_overlap)
assert_allclose(freqs, freqs_2)
assert_allclose(psds[0], psds_2)
with catch_logging() as log:
    psd_array_welch(x, float(n_fft), verbose='debug')
log = log.getvalue()
assert 'using 256-point FFT on 256 samples with 0 overlap' in log
assert 'hamming window' in log
```

## Next Steps


---

*Source: test_psd.py:16 | Complexity: Advanced | Last updated: 2026-05-18*