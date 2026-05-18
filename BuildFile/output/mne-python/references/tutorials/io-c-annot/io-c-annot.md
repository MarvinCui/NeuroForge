# How To: Io C Annot

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test I/O of MNE-C -annot.fif files.

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

### Step 1: 'Test I/O of MNE-C -annot.fif files.'

```python
'Test I/O of MNE-C -annot.fif files.'
```

**Verification:**
```python
assert_array_equal(events_2, events)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw)
```

**Verification:**
```python
assert_allclose(events[:, 0], expected, atol=3)
```

### Step 3: Assign unknown = value

```python
sfreq, first_samp = (raw.info['sfreq'], raw.first_samp)
```

**Verification:**
```python
assert event_id == expected
```

### Step 4: Assign events = read_events(...)

```python
events = read_events(fname_c_annot)
```

### Step 5: Assign unknown = read_events(...)

```python
events_2, event_id = read_events(fname_c_annot, return_event_id=True)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(events_2, events)
```

### Step 7: Assign expected = value

```python
expected = np.arange(2, 5) * sfreq + first_samp
```

### Step 8: Call assert_allclose()

```python
assert_allclose(events[:, 0], expected, atol=3)
```

### Step 9: Assign expected = value

```python
expected = {'Two sec': 1001, 'Three and four sec': 1002}
```

**Verification:**
```python
assert event_id == expected
```


## Complete Example

```python
# Workflow
'Test I/O of MNE-C -annot.fif files.'
raw = read_raw_fif(fname_raw)
sfreq, first_samp = (raw.info['sfreq'], raw.first_samp)
events = read_events(fname_c_annot)
events_2, event_id = read_events(fname_c_annot, return_event_id=True)
assert_array_equal(events_2, events)
expected = np.arange(2, 5) * sfreq + first_samp
assert_allclose(events[:, 0], expected, atol=3)
expected = {'Two sec': 1001, 'Three and four sec': 1002}
assert event_id == expected
```

## Next Steps


---

*Source: test_event.py:204 | Complexity: Advanced | Last updated: 2026-05-18*