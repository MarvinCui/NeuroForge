# How To: Define Events

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test defining response events.

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test defining response events.'

```python
'Test defining response events.'
```

**Verification:**
```python
assert n_target_ == n_target - n_miss
```

### Step 2: Assign events = read_events(...)

```python
events = read_events(fname)
```

**Verification:**
```python
assert_array_equal(true_lag_fill, lag_fill)
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert_array_equal(true_lag_nofill, lag_nofill)
```

### Step 4: Assign unknown = define_target_events(...)

```python
events_, _ = define_target_events(events, 5, 32, raw.info['sfreq'], 0.2, 0.7, 42, 99)
```

### Step 5: Assign n_target = value

```python
n_target = events[events[:, 2] == 5].shape[0]
```

### Step 6: Assign n_miss = value

```python
n_miss = events_[events_[:, 2] == 99].shape[0]
```

### Step 7: Assign n_target_ = value

```python
n_target_ = events_[events_[:, 2] == 42].shape[0]
```

**Verification:**
```python
assert n_target_ == n_target - n_miss
```

### Step 8: Assign events = np.array(...)

```python
events = np.array([[0, 0, 1], [375, 0, 2], [500, 0, 1], [875, 0, 3], [1000, 0, 1], [1375, 0, 3], [1100, 0, 1], [1475, 0, 2], [1500, 0, 1], [1875, 0, 2]])
```

### Step 9: Assign true_lag_nofill = value

```python
true_lag_nofill = [1500.0, 1500.0, 1500.0]
```

### Step 10: Assign true_lag_fill = value

```python
true_lag_fill = [1500.0, np.nan, np.nan, 1500.0, 1500.0]
```

### Step 11: Assign unknown = define_target_events(...)

```python
n, lag_nofill = define_target_events(events, 1, 2, 250.0, 1.4, 1.6, 5)
```

### Step 12: Assign unknown = define_target_events(...)

```python
n, lag_fill = define_target_events(events, 1, 2, 250.0, 1.4, 1.6, 5, 99)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(true_lag_fill, lag_fill)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(true_lag_nofill, lag_nofill)
```


## Complete Example

```python
# Workflow
'Test defining response events.'
events = read_events(fname)
raw = read_raw_fif(raw_fname)
events_, _ = define_target_events(events, 5, 32, raw.info['sfreq'], 0.2, 0.7, 42, 99)
n_target = events[events[:, 2] == 5].shape[0]
n_miss = events_[events_[:, 2] == 99].shape[0]
n_target_ = events_[events_[:, 2] == 42].shape[0]
assert n_target_ == n_target - n_miss
events = np.array([[0, 0, 1], [375, 0, 2], [500, 0, 1], [875, 0, 3], [1000, 0, 1], [1375, 0, 3], [1100, 0, 1], [1475, 0, 2], [1500, 0, 1], [1875, 0, 2]])
true_lag_nofill = [1500.0, 1500.0, 1500.0]
true_lag_fill = [1500.0, np.nan, np.nan, 1500.0, 1500.0]
n, lag_nofill = define_target_events(events, 1, 2, 250.0, 1.4, 1.6, 5)
n, lag_fill = define_target_events(events, 1, 2, 250.0, 1.4, 1.6, 5, 99)
assert_array_equal(true_lag_fill, lag_fill)
assert_array_equal(true_lag_nofill, lag_nofill)
```

## Next Steps


---

*Source: test_event.py:491 | Complexity: Advanced | Last updated: 2026-05-18*