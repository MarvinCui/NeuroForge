# How To: Compute Tfr Correct

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that TFR actually gets us our freq back.

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
# Fixtures: method, decim
```

## Step-by-Step Guide

### Step 1: 'Test that TFR actually gets us our freq back.'

```python
'Test that TFR actually gets us our freq back.'
```

**Verification:**
```python
assert f in freqs
```

### Step 2: Assign sfreq = 1000.0

```python
sfreq = 1000.0
```

**Verification:**
```python
assert freqs[np.argmax(tfr.mean(-1))] == f
```

### Step 3: Assign t = value

```python
t = np.arange(1000) / sfreq
```

### Step 4: Assign f = 50.0

```python
f = 50.0
```

### Step 5: Assign data = np.sin(...)

```python
data = np.sin(2 * np.pi * f * t)
```

### Step 6: Assign data = value

```python
data = data[np.newaxis, np.newaxis]
```

### Step 7: Assign freqs = np.arange(...)

```python
freqs = np.arange(10, 111, 4)
```

**Verification:**
```python
assert f in freqs
```

### Step 8: Assign n_cycles = value

```python
n_cycles = freqs * 0.25
```

### Step 9: Assign tfr = value

```python
tfr = _compute_tfr(data, freqs, sfreq, method=method, decim=decim, n_cycles=n_cycles, output='power')[0, 0]
```

**Verification:**
```python
assert freqs[np.argmax(tfr.mean(-1))] == f
```


## Complete Example

```python
# Setup
# Fixtures: method, decim

# Workflow
'Test that TFR actually gets us our freq back.'
sfreq = 1000.0
t = np.arange(1000) / sfreq
f = 50.0
data = np.sin(2 * np.pi * f * t)
data *= np.hanning(data.size)
data = data[np.newaxis, np.newaxis]
freqs = np.arange(10, 111, 4)
assert f in freqs
n_cycles = freqs * 0.25
tfr = _compute_tfr(data, freqs, sfreq, method=method, decim=decim, n_cycles=n_cycles, output='power')[0, 0]
assert freqs[np.argmax(tfr.mean(-1))] == f
```

## Next Steps


---

*Source: test_tfr.py:1162 | Complexity: Advanced | Last updated: 2026-05-18*