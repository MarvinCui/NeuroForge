# How To: Resample Below 1 Sample

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test resampling doesn't yield datapoints.

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

### Step 1: "Test resampling doesn't yield datapoints."

```python
"Test resampling doesn't yield datapoints."
```

**Verification:**
```python
assert len(raw.times) == 1
```

### Step 2: Assign x = np.zeros(...)

```python
x = np.zeros((1, 100))
```

**Verification:**
```python
assert raw.get_data().shape[1] == 1
```

### Step 3: Assign sfreq = 1000.0

```python
sfreq = 1000.0
```

**Verification:**
```python
assert 'neighborhood' not in log
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(x, create_info(1, sfreq, 'eeg'))
```

**Verification:**
```python
assert 'neighborhood' in log
```

### Step 5: Call raw.resample()

```python
raw.resample(5, method=method)
```

**Verification:**
```python
assert len(epochs.times) == 1
```

### Step 6: Assign x = np.zeros(...)

```python
x = np.zeros((1, 10000))
```

**Verification:**
```python
assert epochs.get_data(copy=False).shape[2] == 1
```

### Step 7: Assign sfreq = 1000.0

```python
sfreq = 1000.0
```

### Step 8: Assign raw = RawArray(...)

```python
raw = RawArray(x, create_info(1, sfreq, 'eeg'))
```

### Step 9: Assign events = np.array(...)

```python
events = np.array([[400, 0, 1], [2000, 0, 1], [3000, 0, 1]])
```

### Step 10: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, {'test': 1}, 0, 0.2, proj=False, picks='eeg', baseline=None, preload=True, verbose=False)
```

### Step 11: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert len(epochs.times) == 1
```

### Step 12: Call epochs.resample()

```python
epochs.resample(1, method=method, verbose=True)
```

**Verification:**
```python
assert 'neighborhood' not in log
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
"Test resampling doesn't yield datapoints."
x = np.zeros((1, 100))
sfreq = 1000.0
raw = RawArray(x, create_info(1, sfreq, 'eeg'))
raw.resample(5, method=method)
assert len(raw.times) == 1
assert raw.get_data().shape[1] == 1
x = np.zeros((1, 10000))
sfreq = 1000.0
raw = RawArray(x, create_info(1, sfreq, 'eeg'))
events = np.array([[400, 0, 1], [2000, 0, 1], [3000, 0, 1]])
epochs = Epochs(raw, events, {'test': 1}, 0, 0.2, proj=False, picks='eeg', baseline=None, preload=True, verbose=False)
with catch_logging() as log:
    epochs.resample(1, method=method, verbose=True)
log = log.getvalue()
if method == 'fft':
    assert 'neighborhood' not in log
else:
    assert 'neighborhood' in log
assert len(epochs.times) == 1
assert epochs.get_data(copy=False).shape[2] == 1
```

## Next Steps


---

*Source: test_filter.py:477 | Complexity: Advanced | Last updated: 2026-05-18*