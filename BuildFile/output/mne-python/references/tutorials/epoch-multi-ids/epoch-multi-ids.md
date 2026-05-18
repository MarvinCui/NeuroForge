# How To: Epoch Multi Ids

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test epoch selection via multiple/partial keys.

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

### Step 1: 'Test epoch selection via multiple/partial keys.'

```python
'Test epoch selection via multiple/partial keys.'
```

**Verification:**
```python
assert_array_equal(epochs_multi.events, epochs_regular.events)
```

### Step 2: Assign unknown = _get_data(...)

```python
raw, events, picks = _get_data()
```

**Verification:**
```python
assert_array_equal(epochs_reverse.events, epochs_regular.events)
```

### Step 3: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, {'a/b/a': 1, 'a/b/b': 2, 'a/c': 3, 'b/d': 4, 'a_b': 5}, tmin, tmax, picks=picks, preload=False)
```

**Verification:**
```python
assert_allclose(epochs_multi.get_data(), epochs_regular.get_data())
```

### Step 4: Assign epochs_regular = value

```python
epochs_regular = epochs['a/b']
```

**Verification:**
```python
assert_allclose(epochs_reverse.get_data(), epochs_regular.get_data())
```

### Step 5: Assign epochs_reverse = value

```python
epochs_reverse = epochs['b/a']
```

### Step 6: Assign epochs_multi = value

```python
epochs_multi = epochs[['a/b/a', 'a/b/b']]
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(epochs_multi.events, epochs_regular.events)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(epochs_reverse.events, epochs_regular.events)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(epochs_multi.get_data(), epochs_regular.get_data())
```

### Step 10: Call assert_allclose()

```python
assert_allclose(epochs_reverse.get_data(), epochs_regular.get_data())
```


## Complete Example

```python
# Workflow
'Test epoch selection via multiple/partial keys.'
raw, events, picks = _get_data()
epochs = Epochs(raw, events, {'a/b/a': 1, 'a/b/b': 2, 'a/c': 3, 'b/d': 4, 'a_b': 5}, tmin, tmax, picks=picks, preload=False)
epochs_regular = epochs['a/b']
epochs_reverse = epochs['b/a']
epochs_multi = epochs[['a/b/a', 'a/b/b']]
assert_array_equal(epochs_multi.events, epochs_regular.events)
assert_array_equal(epochs_reverse.events, epochs_regular.events)
assert_allclose(epochs_multi.get_data(), epochs_regular.get_data())
assert_allclose(epochs_reverse.get_data(), epochs_regular.get_data())
```

## Next Steps


---

*Source: test_epochs.py:1215 | Complexity: Advanced | Last updated: 2026-05-18*