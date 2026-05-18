# How To: Tfr Decim And Shift Time

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test TFR decimation; slices must be long-ish to be longer than the wavelets.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `re`
- `itertools`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.collections`
- `numpy.testing`
- `mne`
- `mne`
- `mne.epochs`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.tfr`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz.utils`
- `test_spectrum`
- `pandas.testing`

**Setup Required:**
```python
# Fixtures: epochs, method, freqs, decim
```

## Step-by-Step Guide

### Step 1: 'Test TFR decimation; slices must be long-ish to be longer than the wavelets.'

```python
'Test TFR decimation; slices must be long-ish to be longer than the wavelets.'
```

**Verification:**
```python
assert tfr.shape[-1] == want
```

### Step 2: Assign tfr = epochs.compute_tfr(...)

```python
tfr = epochs.compute_tfr(method, freqs=freqs, decim=decim)
```

**Verification:**
```python
assert tfr.sfreq == epochs.info['sfreq'] / (decim.step or 1)
```

### Step 3: Assign want = len(...)

```python
want = len(range(*decim.indices(len(epochs.times))))
```

**Verification:**
```python
assert tfr == tfr2
```

### Step 4: Assign shift = value

```python
shift = -0.137
```

**Verification:**
```python
assert_allclose(times + shift, tfr.times, rtol=0, atol=0.5 / tfr.sfreq)
```

### Step 5: Assign unknown = tfr.get_data(...)

```python
data, times, freqs = tfr.get_data(return_times=True, return_freqs=True)
```

**Verification:**
```python
assert_array_equal(data, tfr.get_data())
```

### Step 6: Call tfr.shift_time()

```python
tfr.shift_time(shift, relative=True)
```

**Verification:**
```python
assert_array_equal(freqs, tfr.freqs)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(times + shift, tfr.times, rtol=0, atol=0.5 / tfr.sfreq)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(data, tfr.get_data())
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(freqs, tfr.freqs)
```

### Step 10: Assign decim = slice(...)

```python
decim = slice(None, None, decim)
```

### Step 11: Assign tfr2 = epochs.compute_tfr(...)

```python
tfr2 = epochs.compute_tfr(method, freqs=freqs, decim=1)
```

### Step 12: Call tfr2.decimate()

```python
tfr2.decimate(decim)
```

**Verification:**
```python
assert tfr == tfr2
```


## Complete Example

```python
# Setup
# Fixtures: epochs, method, freqs, decim

# Workflow
'Test TFR decimation; slices must be long-ish to be longer than the wavelets.'
tfr = epochs.compute_tfr(method, freqs=freqs, decim=decim)
if not isinstance(decim, slice):
    decim = slice(None, None, decim)
want = len(range(*decim.indices(len(epochs.times))))
assert tfr.shape[-1] == want
assert tfr.sfreq == epochs.info['sfreq'] / (decim.step or 1)
if isinstance(decim, int):
    tfr2 = epochs.compute_tfr(method, freqs=freqs, decim=1)
    tfr2.decimate(decim)
    assert tfr == tfr2
shift = -0.137
data, times, freqs = tfr.get_data(return_times=True, return_freqs=True)
tfr.shift_time(shift, relative=True)
assert_allclose(times + shift, tfr.times, rtol=0, atol=0.5 / tfr.sfreq)
assert_array_equal(data, tfr.get_data())
assert_array_equal(freqs, tfr.freqs)
```

## Next Steps


---

*Source: test_tfr.py:592 | Complexity: Advanced | Last updated: 2026-05-18*