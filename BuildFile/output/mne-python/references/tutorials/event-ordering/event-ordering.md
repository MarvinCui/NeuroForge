# How To: Event Ordering

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test event order.

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

### Step 1: 'Test event order.'

```python
'Test event order.'
```

**Verification:**
```python
assert_equal(len(Epochs(raw, events2, event_id=dict(a=1), preload=True)), 1)
```

### Step 2: Assign unknown = value

```python
raw, events = _get_data()[:2]
```

### Step 3: Assign events2 = value

```python
events2 = events.copy()[::-1]
```

### Step 4: Call Epochs()

```python
Epochs(raw, events, event_id, tmin, tmax, reject=reject, flat=flat)
```

### Step 5: Assign events2 = value

```python
events2 = events[[0, 0]]
```

### Step 6: Assign unknown = value

```python
events2[:, 2] = [1, 2]
```

### Step 7: Call pytest.raises()

```python
pytest.raises(RuntimeError, Epochs, raw, events2, event_id=None)
```

### Step 8: Call assert_equal()

```python
assert_equal(len(Epochs(raw, events2, event_id=dict(a=1), preload=True)), 1)
```

### Step 9: Call Epochs()

```python
Epochs(raw, events2, event_id, tmin, tmax, reject=reject, flat=flat)
```


## Complete Example

```python
# Workflow
'Test event order.'
raw, events = _get_data()[:2]
events2 = events.copy()[::-1]
Epochs(raw, events, event_id, tmin, tmax, reject=reject, flat=flat)
with pytest.warns(RuntimeWarning, match='chronologically'):
    Epochs(raw, events2, event_id, tmin, tmax, reject=reject, flat=flat)
events2 = events[[0, 0]]
events2[:, 2] = [1, 2]
pytest.raises(RuntimeError, Epochs, raw, events2, event_id=None)
assert_equal(len(Epochs(raw, events2, event_id=dict(a=1), preload=True)), 1)
```

## Next Steps


---

*Source: test_epochs.py:1072 | Complexity: Advanced | Last updated: 2026-05-18*