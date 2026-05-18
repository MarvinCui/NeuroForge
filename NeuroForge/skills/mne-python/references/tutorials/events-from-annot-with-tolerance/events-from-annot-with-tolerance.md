# How To: Events From Annot With Tolerance

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test events_from_annotations w/ and w/o tolerance.

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
# Fixtures: use_rounding, tol, shape, onsets, descriptions
```

## Step-by-Step Guide

### Step 1: 'Test events_from_annotations w/ and w/o tolerance.'

```python
'Test events_from_annotations w/ and w/o tolerance.'
```

**Verification:**
```python
assert events.shape == shape
```

### Step 2: Assign info = create_info(...)

```python
info = create_info(ch_names=1, sfreq=100)
```

**Verification:**
```python
assert (events[:, 0] == onsets).all()
```

### Step 3: Assign raw = RawArray(...)

```python
raw = RawArray(data=np.empty((1, 1000)), info=info, first_samp=0)
```

**Verification:**
```python
assert (events[:, 2] == descriptions).all()
```

### Step 4: Assign meas_date = _handle_meas_date(...)

```python
meas_date = _handle_meas_date(0)
```

### Step 5: Assign chunk_duration = 1

```python
chunk_duration = 1
```

### Step 6: Assign annot = Annotations(...)

```python
annot = Annotations([2.02, 3.02, 4.02], chunk_duration, ['0', '1', '2'], 0)
```

### Step 7: Call raw.set_annotations()

```python
raw.set_annotations(annot)
```

### Step 8: Assign event_id = value

```python
event_id = {'0': 0, '1': 1, '2': 2}
```

**Verification:**
```python
assert events.shape == shape
```

### Step 9: Assign unknown = meas_date

```python
raw.info['meas_date'] = meas_date
```

### Step 10: Assign unknown = events_from_annotations(...)

```python
events, _ = events_from_annotations(raw, event_id=event_id, chunk_duration=chunk_duration)
```

### Step 11: Assign unknown = events_from_annotations(...)

```python
events, _ = events_from_annotations(raw, event_id=event_id, chunk_duration=chunk_duration, use_rounding=use_rounding, tol=tol)
```


## Complete Example

```python
# Setup
# Fixtures: use_rounding, tol, shape, onsets, descriptions

# Workflow
'Test events_from_annotations w/ and w/o tolerance.'
info = create_info(ch_names=1, sfreq=100)
raw = RawArray(data=np.empty((1, 1000)), info=info, first_samp=0)
meas_date = _handle_meas_date(0)
with raw.info._unlock(check_after=True):
    raw.info['meas_date'] = meas_date
chunk_duration = 1
annot = Annotations([2.02, 3.02, 4.02], chunk_duration, ['0', '1', '2'], 0)
raw.set_annotations(annot)
event_id = {'0': 0, '1': 1, '2': 2}
if use_rounding is None:
    events, _ = events_from_annotations(raw, event_id=event_id, chunk_duration=chunk_duration)
else:
    events, _ = events_from_annotations(raw, event_id=event_id, chunk_duration=chunk_duration, use_rounding=use_rounding, tol=tol)
assert events.shape == shape
assert (events[:, 0] == onsets).all()
assert (events[:, 2] == descriptions).all()
```

## Next Steps


---

*Source: test_annotations.py:853 | Complexity: Advanced | Last updated: 2026-05-18*