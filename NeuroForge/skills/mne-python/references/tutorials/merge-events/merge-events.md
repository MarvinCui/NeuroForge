# How To: Merge Events

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test event merging.

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

### Step 1: 'Test event merging.'

```python
'Test event merging.'
```

**Verification:**
```python
assert_array_equal(events, events_good)
```

### Step 2: Assign events_orig = value

```python
events_orig = [[1, 0, 1], [3, 0, 2], [10, 0, 3], [20, 0, 4]]
```

### Step 3: Assign events_replacement = value

```python
events_replacement = [[1, 0, 12], [3, 0, 12], [10, 0, 34], [20, 0, 34]]
```

### Step 4: Assign events_no_replacement = value

```python
events_no_replacement = [[1, 0, 1], [1, 0, 12], [1, 0, 1234], [3, 0, 2], [3, 0, 12], [3, 0, 1234], [10, 0, 3], [10, 0, 34], [10, 0, 1234], [20, 0, 4], [20, 0, 34], [20, 0, 1234]]
```

### Step 5: Assign events = merge_events(...)

```python
events = merge_events(events_orig, [1, 2], 12, replace_events)
```

### Step 6: Assign events = merge_events(...)

```python
events = merge_events(events, [3, 4], 34, replace_events)
```

### Step 7: Assign events = merge_events(...)

```python
events = merge_events(events, [1, 2, 3, 4], 1234, replace_events)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(events, events_good)
```


## Complete Example

```python
# Workflow
'Test event merging.'
events_orig = [[1, 0, 1], [3, 0, 2], [10, 0, 3], [20, 0, 4]]
events_replacement = [[1, 0, 12], [3, 0, 12], [10, 0, 34], [20, 0, 34]]
events_no_replacement = [[1, 0, 1], [1, 0, 12], [1, 0, 1234], [3, 0, 2], [3, 0, 12], [3, 0, 1234], [10, 0, 3], [10, 0, 34], [10, 0, 1234], [20, 0, 4], [20, 0, 34], [20, 0, 1234]]
for replace_events, events_good in [(True, events_replacement), (False, events_no_replacement)]:
    events = merge_events(events_orig, [1, 2], 12, replace_events)
    events = merge_events(events, [3, 4], 34, replace_events)
    events = merge_events(events, [1, 2, 3, 4], 1234, replace_events)
    assert_array_equal(events, events_good)
```

## Next Steps


---

*Source: test_event.py:99 | Complexity: Advanced | Last updated: 2026-05-18*