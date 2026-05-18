# How To: Fix Stim

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test fixing stim STI016 for Neuromag.

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

### Step 1: 'Test fixing stim STI016 for Neuromag.'

```python
'Test fixing stim STI016 for Neuromag.'
```

**Verification:**
```python
assert_array_equal(events[0], [raw.first_samp + 1, 0, 32765])
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=True)
```

**Verification:**
```python
assert_array_equal(events[0], [raw.first_samp + 1, 0, 32771])
```

### Step 3: Assign unknown = value

```python
raw._data[raw.ch_names.index('STI 014'), :3] = [0, -32765, 0]
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(events[0], [raw.first_samp + 1, 0, 32765])
```

### Step 5: Assign events = find_events(...)

```python
events = find_events(raw, 'STI 014', uint_cast=True)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(events[0], [raw.first_samp + 1, 0, 32771])
```

### Step 7: Assign events = find_events(...)

```python
events = find_events(raw, 'STI 014')
```


## Complete Example

```python
# Workflow
'Test fixing stim STI016 for Neuromag.'
raw = read_raw_fif(raw_fname, preload=True)
raw._data[raw.ch_names.index('STI 014'), :3] = [0, -32765, 0]
with pytest.warns(RuntimeWarning, match='STI016'):
    events = find_events(raw, 'STI 014')
assert_array_equal(events[0], [raw.first_samp + 1, 0, 32765])
events = find_events(raw, 'STI 014', uint_cast=True)
assert_array_equal(events[0], [raw.first_samp + 1, 0, 32771])
```

## Next Steps


---

*Source: test_event.py:61 | Complexity: Intermediate | Last updated: 2026-05-18*