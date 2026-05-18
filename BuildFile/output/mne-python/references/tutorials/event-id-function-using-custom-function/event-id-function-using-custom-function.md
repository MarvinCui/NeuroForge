# How To: Event Id Function Using Custom Function

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test [unit_test] arbitrary function to create the ids.

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

### Step 1: 'Test [unit_test] arbitrary function to create the ids.'

```python
'Test [unit_test] arbitrary function to create the ids.'
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
expected_event_id = dict(zip(description, repeat(42)))
```

### Step 4: Assign expected_events = np.repeat(...)

```python
expected_events = np.repeat([[0, 0, 42]], len(description), axis=0)
```

### Step 5: Assign raw = _create_annotation_based_on_descr(...)

```python
raw = _create_annotation_based_on_descr(description)
```

### Step 6: Assign unknown = events_from_annotations(...)

```python
events, event_id = events_from_annotations(raw, event_id=_constant_id)
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
'Test [unit_test] arbitrary function to create the ids.'

def _constant_id(*args, **kwargs):
    return 42
description = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
expected_event_id = dict(zip(description, repeat(42)))
expected_events = np.repeat([[0, 0, 42]], len(description), axis=0)
raw = _create_annotation_based_on_descr(description)
events, event_id = events_from_annotations(raw, event_id=_constant_id)
assert_array_equal(events, expected_events)
assert event_id == expected_event_id
```

## Next Steps


---

*Source: test_annotations.py:954 | Complexity: Intermediate | Last updated: 2026-05-18*