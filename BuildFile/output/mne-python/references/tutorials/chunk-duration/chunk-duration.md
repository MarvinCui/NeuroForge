# How To: Chunk Duration

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test chunk_duration.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `collections`
- `datetime`
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `pytest`
- `mne`
- `mne`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: first_samp
```

## Step-by-Step Guide

### Step 1: 'Test chunk_duration.'

```python
'Test chunk_duration.'
```

**Verification:**
```python
assert raw.annotations.orig_time == raw.info['meas_date']
```

### Step 2: Assign raw = RawArray(...)

```python
raw = RawArray(data=np.empty([10, 10], dtype=np.float64), info=create_info(ch_names=10, sfreq=1.0), first_samp=first_samp)
```

**Verification:**
```python
assert_allclose(raw.annotations.onset, [first_samp])
```

### Step 3: Call raw.set_annotations()

```python
raw.set_annotations(Annotations(description='foo', onset=[0], duration=[10], orig_time=None))
```

**Verification:**
```python
assert_array_equal(events, expected_events)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(raw.annotations.onset, [first_samp])
```

**Verification:**
```python
assert_array_equal(events, expected_events)
```

### Step 5: Assign expected_events = value

```python
expected_events = np.atleast_2d(np.repeat(range(10), repeats=2)).T
```

### Step 6: Assign expected_events = np.insert(...)

```python
expected_events = np.insert(expected_events, 1, 0, axis=1)
```

### Step 7: Assign expected_events = np.insert(...)

```python
expected_events = np.insert(expected_events, 2, 1, axis=1)
```

### Step 8: Assign unknown = events_from_annotations(...)

```python
events, events_id = events_from_annotations(raw, chunk_duration=0.5, use_rounding=False)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(events, expected_events)
```

### Step 10: Assign expected_events = np.zeros(...)

```python
expected_events = np.zeros((3, 3))
```

### Step 11: Assign unknown = 1

```python
expected_events[:, -1] = 1
```

### Step 12: Assign unknown = value

```python
expected_events[:, 0] = np.arange(0, 9, step=3) + first_samp
```

### Step 13: Assign unknown = events_from_annotations(...)

```python
events, events_id = events_from_annotations(raw, chunk_duration=3.0)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(events, expected_events)
```

### Step 15: Assign unknown = _handle_meas_date(...)

```python
raw.info['meas_date'] = _handle_meas_date(0)
```


## Complete Example

```python
# Setup
# Fixtures: first_samp

# Workflow
'Test chunk_duration.'
raw = RawArray(data=np.empty([10, 10], dtype=np.float64), info=create_info(ch_names=10, sfreq=1.0), first_samp=first_samp)
with raw.info._unlock():
    raw.info['meas_date'] = _handle_meas_date(0)
raw.set_annotations(Annotations(description='foo', onset=[0], duration=[10], orig_time=None))
assert raw.annotations.orig_time == raw.info['meas_date']
assert_allclose(raw.annotations.onset, [first_samp])
expected_events = np.atleast_2d(np.repeat(range(10), repeats=2)).T
expected_events = np.insert(expected_events, 1, 0, axis=1)
expected_events = np.insert(expected_events, 2, 1, axis=1)
expected_events[:, 0] += first_samp
events, events_id = events_from_annotations(raw, chunk_duration=0.5, use_rounding=False)
assert_array_equal(events, expected_events)
expected_events = np.zeros((3, 3))
expected_events[:, -1] = 1
expected_events[:, 0] = np.arange(0, 9, step=3) + first_samp
events, events_id = events_from_annotations(raw, chunk_duration=3.0)
assert_array_equal(events, expected_events)
```

## Next Steps


---

*Source: test_annotations.py:302 | Complexity: Advanced | Last updated: 2026-05-18*