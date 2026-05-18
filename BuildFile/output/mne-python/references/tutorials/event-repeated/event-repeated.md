# How To: Event Repeated

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test epochs takes into account repeated events.

## Prerequisites

**Required Modules:**
- `pickle`
- `copy`
- `datetime`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `scipy.signal`
- `numpy.fft`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.proj`
- `mne._fiff.write`
- `mne.annotations`
- `mne.baseline`
- `mne.chpi`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`
- `pandas.testing`
- `pandas`
- `pandas`


## Step-by-Step Guide

### Step 1: 'Test epochs takes into account repeated events.'

```python
'Test epochs takes into account repeated events.'
```

**Verification:**
```python
assert epochs.drop_log == ((), ('DROP DUPLICATE',))
```

### Step 2: Assign n_samples = 100

```python
n_samples = 100
```

**Verification:**
```python
assert_array_equal(epochs.selection, [0])
```

### Step 3: Assign n_channels = 2

```python
n_channels = 2
```

**Verification:**
```python
assert epochs.drop_log == ((), ('MERGE DUPLICATE',))
```

### Step 4: Assign ch_names = value

```python
ch_names = [f'chan{i}' for i in range(n_channels)]
```

**Verification:**
```python
assert_array_equal(epochs.selection, [0])
```

### Step 5: Assign info = mne.create_info(...)

```python
info = mne.create_info(ch_names=ch_names, sfreq=1000.0)
```

### Step 6: Assign data = np.zeros(...)

```python
data = np.zeros((n_channels, n_samples))
```

### Step 7: Assign raw = mne.io.RawArray(...)

```python
raw = mne.io.RawArray(data, info)
```

### Step 8: Assign events = np.array(...)

```python
events = np.array([[10, 0, 1], [10, 0, 2]])
```

### Step 9: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, event_repeated='drop')
```

**Verification:**
```python
assert epochs.drop_log == ((), ('DROP DUPLICATE',))
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(epochs.selection, [0])
```

### Step 11: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, event_repeated='merge')
```

**Verification:**
```python
assert epochs.drop_log == ((), ('MERGE DUPLICATE',))
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(epochs.selection, [0])
```


## Complete Example

```python
# Workflow
'Test epochs takes into account repeated events.'
n_samples = 100
n_channels = 2
ch_names = [f'chan{i}' for i in range(n_channels)]
info = mne.create_info(ch_names=ch_names, sfreq=1000.0)
data = np.zeros((n_channels, n_samples))
raw = mne.io.RawArray(data, info)
events = np.array([[10, 0, 1], [10, 0, 2]])
epochs = mne.Epochs(raw, events, event_repeated='drop')
assert epochs.drop_log == ((), ('DROP DUPLICATE',))
assert_array_equal(epochs.selection, [0])
epochs = mne.Epochs(raw, events, event_repeated='merge')
assert epochs.drop_log == ((), ('MERGE DUPLICATE',))
assert_array_equal(epochs.selection, [0])
```

## Next Steps


---

*Source: test_epochs.py:117 | Complexity: Advanced | Last updated: 2026-05-18*