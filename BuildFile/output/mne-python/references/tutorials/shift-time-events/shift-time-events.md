# How To: Shift Time Events

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test events latency shift by a given amount.

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

### Step 1: 'Test events latency shift by a given amount.'

```python
'Test events latency shift by a given amount.'
```

**Verification:**
```python
assert all(new_events[:, 0] == EXPECTED)
```

### Step 2: Assign events = np.array(...)

```python
events = np.array([[0, 0, 0], [1, 1, 1], [2, 2, 2]])
```

**Verification:**
```python
assert all(new_events[:, 0] == EXPECTED)
```

### Step 3: Assign EXPECTED = value

```python
EXPECTED = [1, 2, 3]
```

### Step 4: Assign new_events = shift_time_events(...)

```python
new_events = shift_time_events(events, ids=None, tshift=1, sfreq=1)
```

**Verification:**
```python
assert all(new_events[:, 0] == EXPECTED)
```

### Step 5: Assign events = np.array(...)

```python
events = np.array([[0, 0, 0], [1, 1, 1], [2, 2, 2]])
```

### Step 6: Assign EXPECTED = value

```python
EXPECTED = [0, 2, 3]
```

### Step 7: Assign new_events = shift_time_events(...)

```python
new_events = shift_time_events(events, ids=[1, 2], tshift=1, sfreq=1)
```

**Verification:**
```python
assert all(new_events[:, 0] == EXPECTED)
```


## Complete Example

```python
# Workflow
'Test events latency shift by a given amount.'
events = np.array([[0, 0, 0], [1, 1, 1], [2, 2, 2]])
EXPECTED = [1, 2, 3]
new_events = shift_time_events(events, ids=None, tshift=1, sfreq=1)
assert all(new_events[:, 0] == EXPECTED)
events = np.array([[0, 0, 0], [1, 1, 1], [2, 2, 2]])
EXPECTED = [0, 2, 3]
new_events = shift_time_events(events, ids=[1, 2], tshift=1, sfreq=1)
assert all(new_events[:, 0] == EXPECTED)
```

## Next Steps


---

*Source: test_event.py:601 | Complexity: Intermediate | Last updated: 2026-05-18*