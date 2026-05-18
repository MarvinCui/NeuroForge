# How To: Epochs Hash

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test epoch hashing.

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

### Step 1: 'Test epoch hashing.'

```python
'Test epoch hashing.'
```

**Verification:**
```python
assert_equal(hash(epochs), hash(epochs))
```

### Step 2: Assign unknown = value

```python
raw, events = _get_data()[:2]
```

**Verification:**
```python
assert_equal(hash(epochs), hash(epochs_2))
```

### Step 3: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax)
```

**Verification:**
```python
assert pickle.dumps(epochs) == pickle.dumps(epochs_2)
```

### Step 4: Call pytest.raises()

```python
pytest.raises(RuntimeError, epochs.__hash__)
```

**Verification:**
```python
assert hash(epochs) != hash(epochs_2)
```

### Step 5: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, preload=True)
```

### Step 6: Call assert_equal()

```python
assert_equal(hash(epochs), hash(epochs))
```

### Step 7: Assign epochs_2 = Epochs(...)

```python
epochs_2 = Epochs(raw, events, event_id, tmin, tmax, preload=True)
```

### Step 8: Call assert_equal()

```python
assert_equal(hash(epochs), hash(epochs_2))
```

**Verification:**
```python
assert pickle.dumps(epochs) == pickle.dumps(epochs_2)
```


## Complete Example

```python
# Workflow
'Test epoch hashing.'
raw, events = _get_data()[:2]
epochs = Epochs(raw, events, event_id, tmin, tmax)
pytest.raises(RuntimeError, epochs.__hash__)
epochs = Epochs(raw, events, event_id, tmin, tmax, preload=True)
assert_equal(hash(epochs), hash(epochs))
epochs_2 = Epochs(raw, events, event_id, tmin, tmax, preload=True)
assert_equal(hash(epochs), hash(epochs_2))
assert pickle.dumps(epochs) == pickle.dumps(epochs_2)
epochs_2._data[0, 0, 0] -= 1
assert hash(epochs) != hash(epochs_2)
```

## Next Steps


---

*Source: test_epochs.py:1056 | Complexity: Advanced | Last updated: 2026-05-18*