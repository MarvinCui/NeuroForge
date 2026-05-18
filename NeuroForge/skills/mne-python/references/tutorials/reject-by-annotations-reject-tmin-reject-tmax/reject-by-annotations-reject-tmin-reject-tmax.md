# How To: Reject By Annotations Reject Tmin Reject Tmax

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reject_by_annotations with reject_tmin and reject_tmax defined.

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

### Step 1: 'Test reject_by_annotations with reject_tmin and reject_tmax defined.'

```python
'Test reject_by_annotations with reject_tmin and reject_tmax defined.'
```

**Verification:**
```python
assert len(epochs) == 0
```

### Step 2: Assign info = mne.create_info(...)

```python
info = mne.create_info(ch_names=['test_a'], sfreq=1000, ch_types='eeg')
```

**Verification:**
```python
assert len(epochs) == 1
```

### Step 3: Assign raw = mne.io.RawArray(...)

```python
raw = mne.io.RawArray(np.atleast_2d(np.arange(0, 10, 1 / 1000)), info=info)
```

**Verification:**
```python
assert len(epochs) == 1
```

### Step 4: Assign events = np.array(...)

```python
events = np.array([[2000, 0, 1]])
```

### Step 5: Call raw.set_annotations()

```python
raw.set_annotations(mne.Annotations(1, 0.5, 'BAD'))
```

**Verification:**
```python
assert len(epochs) == 0
```

### Step 6: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, tmin=-1, tmax=1, reject_tmin=-0.2, preload=True, reject_by_annotation=True)
```

**Verification:**
```python
assert len(epochs) == 1
```

### Step 7: Call raw.set_annotations()

```python
raw.set_annotations(mne.Annotations(2.5, 0.5, 'BAD'))
```

### Step 8: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, tmin=-1, tmax=1, reject_tmax=0.4, preload=True, reject_by_annotation=True)
```

**Verification:**
```python
assert len(epochs) == 1
```

### Step 9: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, tmin=-1, tmax=1, preload=True, reject_by_annotation=True)
```


## Complete Example

```python
# Workflow
'Test reject_by_annotations with reject_tmin and reject_tmax defined.'
info = mne.create_info(ch_names=['test_a'], sfreq=1000, ch_types='eeg')
raw = mne.io.RawArray(np.atleast_2d(np.arange(0, 10, 1 / 1000)), info=info)
events = np.array([[2000, 0, 1]])
raw.set_annotations(mne.Annotations(1, 0.5, 'BAD'))
with pytest.warns(RuntimeWarning, match='were dropped'):
    epochs = mne.Epochs(raw, events, tmin=-1, tmax=1, preload=True, reject_by_annotation=True)
assert len(epochs) == 0
epochs = mne.Epochs(raw, events, tmin=-1, tmax=1, reject_tmin=-0.2, preload=True, reject_by_annotation=True)
assert len(epochs) == 1
raw.set_annotations(mne.Annotations(2.5, 0.5, 'BAD'))
epochs = mne.Epochs(raw, events, tmin=-1, tmax=1, reject_tmax=0.4, preload=True, reject_by_annotation=True)
assert len(epochs) == 1
```

## Next Steps


---

*Source: test_epochs.py:764 | Complexity: Advanced | Last updated: 2026-05-18*