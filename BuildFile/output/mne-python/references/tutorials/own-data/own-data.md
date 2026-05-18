# How To: Own Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test for epochs data ownership (gh-5346).

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

### Step 1: 'Test for epochs data ownership (gh-5346).'

```python
'Test for epochs data ownership (gh-5346).'
```

**Verification:**
```python
assert epochs._data.flags['C_CONTIGUOUS']
```

### Step 2: Assign unknown = value

```python
raw, events = _get_data()[:2]
```

**Verification:**
```python
assert epochs._data.flags['OWNDATA']
```

### Step 3: Assign n_epochs = 10

```python
n_epochs = 10
```

**Verification:**
```python
assert len(epochs) == epochs._data.shape[0] == len(epochs.events)
```

### Step 4: Assign events = value

```python
events = events[:n_epochs]
```

**Verification:**
```python
assert len(epochs) == n_epochs
```

### Step 5: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, preload=True)
```

**Verification:**
```python
assert not epochs._data.flags['OWNDATA']
```

### Step 6: Call epochs.crop()

```python
epochs.crop(tmin=-0.1, tmax=0.4)
```

**Verification:**
```python
assert 5 < n_now < n_epochs
```

### Step 7: Call epochs.drop_bad()

```python
epochs.drop_bad(flat=dict(eeg=8e-06))
```

**Verification:**
```python
assert len(epochs) == epochs._data.shape[0] == len(epochs.events)
```

### Step 8: Assign n_now = len(...)

```python
n_now = len(epochs)
```

**Verification:**
```python
assert 1 < len(epochs) < n_now
```

### Step 9: Assign good_chan = epochs.copy.pick(...)

```python
good_chan = epochs.copy().pick([epochs.ch_names[0]])
```

### Step 10: Call good_chan.rename_channels()

```python
good_chan.rename_channels({good_chan.ch_names[0]: 'good'})
```

### Step 11: Call epochs.add_channels()

```python
epochs.add_channels([good_chan])
```

### Step 12: Call epochs.drop_bad()

```python
epochs.drop_bad(flat=dict(eeg=1e-05))
```

**Verification:**
```python
assert 1 < len(epochs) < n_now
```


## Complete Example

```python
# Workflow
'Test for epochs data ownership (gh-5346).'
raw, events = _get_data()[:2]
n_epochs = 10
events = events[:n_epochs]
epochs = mne.Epochs(raw, events, preload=True)
assert epochs._data.flags['C_CONTIGUOUS']
assert epochs._data.flags['OWNDATA']
epochs.crop(tmin=-0.1, tmax=0.4)
assert len(epochs) == epochs._data.shape[0] == len(epochs.events)
assert len(epochs) == n_epochs
assert not epochs._data.flags['OWNDATA']
epochs.drop_bad(flat=dict(eeg=8e-06))
n_now = len(epochs)
assert 5 < n_now < n_epochs
assert len(epochs) == epochs._data.shape[0] == len(epochs.events)
good_chan = epochs.copy().pick([epochs.ch_names[0]])
good_chan.rename_channels({good_chan.ch_names[0]: 'good'})
epochs.add_channels([good_chan])
epochs.drop_bad(flat=dict(eeg=1e-05))
assert 1 < len(epochs) < n_now
```

## Next Steps


---

*Source: test_epochs.py:806 | Complexity: Advanced | Last updated: 2026-05-18*