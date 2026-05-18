# How To: Find Events Backward Compatibility

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if events are detected correctly in a typical MNE workflow.

## Prerequisites

**Required Modules:**
- `datetime`
- `contextlib`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.pick`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.edf.edf`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test if events are detected correctly in a typical MNE workflow.'

```python
'Test if events are detected correctly in a typical MNE workflow.'
```

**Verification:**
```python
assert_array_equal(events_from_EFA, EXPECTED_EVENTS)
```

### Step 2: Assign EXPECTED_EVENTS = value

```python
EXPECTED_EVENTS = [[68, 0, 2], [199, 0, 2], [1024, 0, 3], [1280, 0, 2]]
```

### Step 3: Assign raw = read_raw_edf(...)

```python
raw = read_raw_edf(edf_path, preload=True)
```

### Step 4: Assign event_id = value

```python
event_id = {a: n for n, a in enumerate(sorted(set(raw.annotations.description)), start=1)}
```

### Step 5: Call event_id.pop()

```python
event_id.pop('start')
```

### Step 6: Assign unknown = events_from_annotations(...)

```python
events_from_EFA, _ = events_from_annotations(raw, event_id=event_id, use_rounding=False)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(events_from_EFA, EXPECTED_EVENTS)
```


## Complete Example

```python
# Workflow
'Test if events are detected correctly in a typical MNE workflow.'
EXPECTED_EVENTS = [[68, 0, 2], [199, 0, 2], [1024, 0, 3], [1280, 0, 2]]
raw = read_raw_edf(edf_path, preload=True)
event_id = {a: n for n, a in enumerate(sorted(set(raw.annotations.description)), start=1)}
event_id.pop('start')
events_from_EFA, _ = events_from_annotations(raw, event_id=event_id, use_rounding=False)
assert_array_equal(events_from_EFA, EXPECTED_EVENTS)
```

## Next Steps


---

*Source: test_edf.py:376 | Complexity: Intermediate | Last updated: 2026-05-18*