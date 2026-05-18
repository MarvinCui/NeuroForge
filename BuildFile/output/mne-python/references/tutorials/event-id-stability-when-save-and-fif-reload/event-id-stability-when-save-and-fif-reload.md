# How To: Event Id Stability When Save And Fif Reload

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test load events from brainvision annotations when read_raw_fif.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `configparser`
- `datetime`
- `inspect`
- `re`
- `shutil`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test load events from brainvision annotations when read_raw_fif.'

```python
'Test load events from brainvision annotations when read_raw_fif.'
```

**Verification:**
```python
assert event_id == original_event_id
```

### Step 2: Assign fname = value

```python
fname = tmp_path / 'bv-raw.fif'
```

**Verification:**
```python
assert_array_equal(events, original_events)
```

### Step 3: Assign raw = read_raw_brainvision(...)

```python
raw = read_raw_brainvision(vhdr_path, eog=eog)
```

### Step 4: Assign unknown = events_from_annotations(...)

```python
original_events, original_event_id = events_from_annotations(raw)
```

### Step 5: Call raw.save()

```python
raw.save(fname)
```

### Step 6: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname)
```

### Step 7: Assign unknown = events_from_annotations(...)

```python
events, event_id = events_from_annotations(raw)
```

**Verification:**
```python
assert event_id == original_event_id
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(events, original_events)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test load events from brainvision annotations when read_raw_fif.'
fname = tmp_path / 'bv-raw.fif'
raw = read_raw_brainvision(vhdr_path, eog=eog)
original_events, original_event_id = events_from_annotations(raw)
raw.save(fname)
raw = read_raw_fif(fname)
events, event_id = events_from_annotations(raw)
assert event_id == original_event_id
assert_array_equal(events, original_events)
```

## Next Steps


---

*Source: test_brainvision.py:1034 | Complexity: Advanced | Last updated: 2026-05-18*