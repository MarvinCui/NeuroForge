# How To: Event Id Function Default

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test[unit_test] for event_id_function default in event_from_annotations.

The expected behavior is give numeric label for all those annotations not
present in event_id, starting at 1.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test[unit_test] for event_id_function default in event_from_annotations.\n\n    The expected behavior is give numeric label for all those annotations not\n    present in event_id, starting at 1.\n    '

```python
'Test[unit_test] for event_id_function default in event_from_annotations.\n\n    The expected behavior is give numeric label for all those annotations not\n    present in event_id, starting at 1.\n    '
```

**Verification:**
```python
assert_array_equal(events, expected_events)
```

### Step 2: Assign description = value

```python
description = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
```

**Verification:**
```python
assert event_id == expected_event_id
```

### Step 3: Assign expected_event_id = dict(...)

```python
expected_event_id = dict(zip(description, range(1, 100)))
```

### Step 4: Assign expected_events = value

```python
expected_events = np.array([[3, 3, 3, 3, 3, 3, 3], [0, 0, 0, 0, 0, 0, 0], [1, 2, 3, 4, 5, 6, 7]]).T
```

### Step 5: Assign raw = _create_annotation_based_on_descr(...)

```python
raw = _create_annotation_based_on_descr(description, annotation_start_sampl=3, duration=100)
```

### Step 6: Assign unknown = events_from_annotations(...)

```python
events, event_id = events_from_annotations(raw, event_id=None)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(events, expected_events)
```

**Verification:**
```python
assert event_id == expected_event_id
```


## Complete Example

```python
# Workflow
'Test[unit_test] for event_id_function default in event_from_annotations.\n\n    The expected behavior is give numeric label for all those annotations not\n    present in event_id, starting at 1.\n    '
description = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
expected_event_id = dict(zip(description, range(1, 100)))
expected_events = np.array([[3, 3, 3, 3, 3, 3, 3], [0, 0, 0, 0, 0, 0, 0], [1, 2, 3, 4, 5, 6, 7]]).T
raw = _create_annotation_based_on_descr(description, annotation_start_sampl=3, duration=100)
events, event_id = events_from_annotations(raw, event_id=None)
assert_array_equal(events, expected_events)
assert event_id == expected_event_id
```

## Next Steps


---

*Source: test_annotations.py:932 | Complexity: Intermediate | Last updated: 2026-05-18*