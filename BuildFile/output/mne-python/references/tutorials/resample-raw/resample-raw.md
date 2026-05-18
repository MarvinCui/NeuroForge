# How To: Resample Raw

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test resampling using RawArray.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.fft`
- `numpy.testing`
- `scipy.signal`
- `scipy.signal`
- `mne`
- `mne._fiff.pick`
- `mne.filter`
- `mne.io`
- `mne.utils`
- `mne.cuda`

**Setup Required:**
```python
# Fixtures: method
```

## Step-by-Step Guide

### Step 1: 'Test resampling using RawArray.'

```python
'Test resampling using RawArray.'
```

**Verification:**
```python
assert data.shape == (1, 63)
```

### Step 2: Assign x = np.zeros(...)

```python
x = np.zeros((1, 1001))
```

### Step 3: Assign sfreq = 2048.0

```python
sfreq = 2048.0
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(x, create_info(1, sfreq, 'eeg'))
```

### Step 5: Call raw.resample()

```python
raw.resample(128, npad=10, method=method)
```

### Step 6: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

**Verification:**
```python
assert data.shape == (1, 63)
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
'Test resampling using RawArray.'
x = np.zeros((1, 1001))
sfreq = 2048.0
raw = RawArray(x, create_info(1, sfreq, 'eeg'))
raw.resample(128, npad=10, method=method)
data = raw.get_data()
assert data.shape == (1, 63)
```

## Next Steps


---

*Source: test_filter.py:466 | Complexity: Intermediate | Last updated: 2026-05-18*