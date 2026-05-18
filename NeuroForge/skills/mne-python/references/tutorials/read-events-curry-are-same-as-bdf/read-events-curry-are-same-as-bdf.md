# How To: Read Events Curry Are Same As Bdf

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test events from curry annotations recovers the right events.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne._fiff.constants`
- `mne._fiff.tag`
- `mne.annotations`
- `mne.bem`
- `mne.channels`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.io.bti`
- `mne.io.curry`
- `mne.io.curry.curry`
- `mne.io.edf`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname
```

## Step-by-Step Guide

### Step 1: 'Test events from curry annotations recovers the right events.'

```python
'Test events from curry annotations recovers the right events.'
```

**Verification:**
```python
assert_allclose(events, REF_EVENTS)
```

### Step 2: Assign EVENT_ID = value

```python
EVENT_ID = {str(ii): ii for ii in range(5)}
```

**Verification:**
```python
assert not raw.info['dev_head_t']
```

### Step 3: Assign REF_EVENTS = find_events(...)

```python
REF_EVENTS = find_events(read_raw_bdf(bdf_file, preload=True))
```

### Step 4: Assign raw = read_raw_curry(...)

```python
raw = read_raw_curry(fname)
```

### Step 5: Assign unknown = events_from_annotations(...)

```python
events, _ = events_from_annotations(raw, event_id=EVENT_ID)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(events, REF_EVENTS)
```

**Verification:**
```python
assert not raw.info['dev_head_t']
```


## Complete Example

```python
# Setup
# Fixtures: fname

# Workflow
'Test events from curry annotations recovers the right events.'
EVENT_ID = {str(ii): ii for ii in range(5)}
REF_EVENTS = find_events(read_raw_bdf(bdf_file, preload=True))
raw = read_raw_curry(fname)
events, _ = events_from_annotations(raw, event_id=EVENT_ID)
assert_allclose(events, REF_EVENTS)
assert not raw.info['dev_head_t']
```

## Next Steps


---

*Source: test_curry.py:348 | Complexity: Intermediate | Last updated: 2026-05-18*