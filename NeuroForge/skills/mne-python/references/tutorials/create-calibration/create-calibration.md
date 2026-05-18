# How To: Create Calibration

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test creating a Calibration object.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `mne.datasets.testing`
- `calibration`
- `matplotlib.pyplot`

**Setup Required:**
```python
# Fixtures: onset, model, eye, avg_error, max_error, positions, offsets, gaze, screen_size, screen_distance, screen_resolution
```

## Step-by-Step Guide

### Step 1: 'Test creating a Calibration object.'

```python
'Test creating a Calibration object.'
```

**Verification:**
```python
assert cal['onset'] == onset
```

### Step 2: Assign kwargs = dict(...)

```python
kwargs = dict(onset=onset, model=model, eye=eye, avg_error=avg_error, max_error=max_error, positions=positions, offsets=offsets, gaze=gaze, screen_size=screen_size, screen_distance=screen_distance, screen_resolution=screen_resolution)
```

**Verification:**
```python
assert cal['model'] == model
```

### Step 3: Assign cal = Calibration(...)

```python
cal = Calibration(**kwargs)
```

**Verification:**
```python
assert cal['eye'] == eye
```

### Step 4: Assign copied_obj = cal.copy(...)

```python
copied_obj = cal.copy()
```

**Verification:**
```python
assert cal['avg_error'] == avg_error
```

### Step 5: Assign unknown = 20

```python
copied_obj['onset'] = 20
```

**Verification:**
```python
assert cal['max_error'] == max_error
```


## Complete Example

```python
# Setup
# Fixtures: onset, model, eye, avg_error, max_error, positions, offsets, gaze, screen_size, screen_distance, screen_resolution

# Workflow
'Test creating a Calibration object.'
kwargs = dict(onset=onset, model=model, eye=eye, avg_error=avg_error, max_error=max_error, positions=positions, offsets=offsets, gaze=gaze, screen_size=screen_size, screen_distance=screen_distance, screen_resolution=screen_resolution)
cal = Calibration(**kwargs)
assert cal['onset'] == onset
assert cal['model'] == model
assert cal['eye'] == eye
assert cal['avg_error'] == avg_error
assert cal['max_error'] == max_error
if positions is not None:
    assert isinstance(cal['positions'], np.ndarray)
    assert np.array_equal(cal['positions'], np.array(POSITIONS))
else:
    assert cal['positions'] is None
if offsets is not None:
    assert isinstance(cal['offsets'], np.ndarray)
    assert np.array_equal(cal['offsets'], np.array(OFFSETS))
if gaze is not None:
    assert isinstance(cal['gaze'], np.ndarray)
    assert np.array_equal(cal['gaze'], np.array(GAZES))
assert cal['screen_size'] == screen_size
assert cal['screen_distance'] == screen_distance
assert cal['screen_resolution'] == screen_resolution
copied_obj = cal.copy()
assert isinstance(copied_obj, Calibration)
assert copied_obj['onset'] == cal['onset']
copied_obj['onset'] = 20
assert copied_obj['onset'] != cal['onset']
if cal['onset'] is not None:
    assert repr(cal) == EXPECTED_REPR
```

## Next Steps


---

*Source: test_calibration.py:58 | Complexity: Intermediate | Last updated: 2026-05-18*