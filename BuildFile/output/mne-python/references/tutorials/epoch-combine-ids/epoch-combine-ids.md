# How To: Epoch Combine Ids

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test combining event ids in epochs compared to events.

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

### Step 1: 'Test combining event ids in epochs compared to events.'

```python
'Test combining event ids in epochs compared to events.'
```

**Verification:**
```python
assert_equal(epochs_new['ab']._name, 'ab')
```

### Step 2: Assign unknown = _get_data(...)

```python
raw, events, picks = _get_data()
```

**Verification:**
```python
assert_array_equal(events_new, epochs_new.events)
```

### Step 3: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5, 'f': 32}, tmin, tmax, picks=picks, preload=False)
```

### Step 4: Assign events_new = merge_events(...)

```python
events_new = merge_events(events, [1, 2], 12)
```

### Step 5: Assign epochs_new = combine_event_ids(...)

```python
epochs_new = combine_event_ids(epochs, ['a', 'b'], {'ab': 12})
```

### Step 6: Call assert_equal()

```python
assert_equal(epochs_new['ab']._name, 'ab')
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(events_new, epochs_new.events)
```


## Complete Example

```python
# Workflow
'Test combining event ids in epochs compared to events.'
raw, events, picks = _get_data()
epochs = Epochs(raw, events, {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5, 'f': 32}, tmin, tmax, picks=picks, preload=False)
events_new = merge_events(events, [1, 2], 12)
epochs_new = combine_event_ids(epochs, ['a', 'b'], {'ab': 12})
assert_equal(epochs_new['ab']._name, 'ab')
assert_array_equal(events_new, epochs_new.events)
```

## Next Steps


---

*Source: test_epochs.py:1196 | Complexity: Intermediate | Last updated: 2026-05-18*