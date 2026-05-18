# How To: Savgol Filter

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test savgol filtering.

## Prerequisites

**Required Modules:**
- `pickle`
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.evoked`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test savgol filtering.'

```python
'Test savgol filtering.'
```

**Verification:**
```python
assert_allclose(np.mean(data[:, match_mask], 0), np.mean(data_filt[:, match_mask], 0), rtol=0.0001, atol=0.01)
```

### Step 2: Assign h_freq = 10.0

```python
h_freq = 10.0
```

**Verification:**
```python
assert np.mean(data[:, mismatch_mask]) > np.mean(data_filt[:, mismatch_mask]) * 5
```

### Step 3: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(fname, 0)
```

**Verification:**
```python
assert_allclose(data, np.abs(fftpack.fft(evoked.data)), atol=1e-16)
```

### Step 4: Assign freqs = fftpack.fftfreq(...)

```python
freqs = fftpack.fftfreq(len(evoked.times), 1.0 / evoked.info['sfreq'])
```

### Step 5: Assign data = np.abs(...)

```python
data = np.abs(fftpack.fft(evoked.data))
```

### Step 6: Assign match_mask = np.logical_and(...)

```python
match_mask = np.logical_and(freqs >= 0, freqs <= h_freq / 2.0)
```

### Step 7: Assign mismatch_mask = np.logical_and(...)

```python
mismatch_mask = np.logical_and(freqs >= h_freq * 2, freqs < 50.0)
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, evoked.savgol_filter, evoked.info['sfreq'])
```

### Step 9: Assign evoked_sg = evoked.copy.savgol_filter(...)

```python
evoked_sg = evoked.copy().savgol_filter(h_freq)
```

### Step 10: Assign data_filt = np.abs(...)

```python
data_filt = np.abs(fftpack.fft(evoked_sg.data))
```

### Step 11: Call assert_allclose()

```python
assert_allclose(np.mean(data[:, match_mask], 0), np.mean(data_filt[:, match_mask], 0), rtol=0.0001, atol=0.01)
```

**Verification:**
```python
assert np.mean(data[:, mismatch_mask]) > np.mean(data_filt[:, mismatch_mask]) * 5
```

### Step 12: Call assert_allclose()

```python
assert_allclose(data, np.abs(fftpack.fft(evoked.data)), atol=1e-16)
```


## Complete Example

```python
# Workflow
'Test savgol filtering.'
h_freq = 10.0
evoked = read_evokeds(fname, 0)
freqs = fftpack.fftfreq(len(evoked.times), 1.0 / evoked.info['sfreq'])
data = np.abs(fftpack.fft(evoked.data))
match_mask = np.logical_and(freqs >= 0, freqs <= h_freq / 2.0)
mismatch_mask = np.logical_and(freqs >= h_freq * 2, freqs < 50.0)
pytest.raises(ValueError, evoked.savgol_filter, evoked.info['sfreq'])
evoked_sg = evoked.copy().savgol_filter(h_freq)
data_filt = np.abs(fftpack.fft(evoked_sg.data))
assert_allclose(np.mean(data[:, match_mask], 0), np.mean(data_filt[:, match_mask], 0), rtol=0.0001, atol=0.01)
assert np.mean(data[:, mismatch_mask]) > np.mean(data_filt[:, mismatch_mask]) * 5
assert_allclose(data, np.abs(fftpack.fft(evoked.data)), atol=1e-16)
```

## Next Steps


---

*Source: test_evoked.py:143 | Complexity: Advanced | Last updated: 2026-05-18*