# How To: Check Events Warnings

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the function which tests that the events        data describes a valid experimental paradigm.
    

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `numpy.testing`
- `nilearn._utils.data_gen`
- `nilearn.glm.first_level.experimental_paradigm`
- `_testing`


## Step-by-Step Guide

### Step 1: 'Test the function which tests that the events        data describes a valid experimental paradigm.\n    '

```python
'Test the function which tests that the events        data describes a valid experimental paradigm.\n    '
```

**Verification:**
```python
assert len(np.unique(events_copy['trial_type'])) == 1
```

### Step 2: Assign events = basic_paradigm(...)

```python
events = basic_paradigm()
```

**Verification:**
```python
assert events_copy['trial_type'][0] == 'dummy'
```

### Step 3: Assign events = events.drop(...)

```python
events = events.drop(columns=['trial_type'])
```

**Verification:**
```python
assert_array_equal(events_copy['trial_type'], events_copy2['trial_type'])
```

### Step 4: Assign unknown = np.zeros(...)

```python
events['foo'] = np.zeros(len(events))
```

**Verification:**
```python
assert_array_equal(events_copy['onset'], events_copy2['onset'])
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(events_copy['trial_type'], events_copy2['trial_type'])
```

**Verification:**
```python
assert_array_equal(events_copy['duration'], events_copy2['duration'])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(events_copy['onset'], events_copy2['onset'])
```

**Verification:**
```python
assert_array_equal(events_copy['modulation'], events_copy2['modulation'])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(events_copy['duration'], events_copy2['duration'])
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(events_copy['modulation'], events_copy2['modulation'])
```

### Step 9: Assign events_copy = check_events(...)

```python
events_copy = check_events(events)
```

### Step 10: Assign events_copy2 = check_events(...)

```python
events_copy2 = check_events(events)
```


## Complete Example

```python
# Workflow
'Test the function which tests that the events        data describes a valid experimental paradigm.\n    '
events = basic_paradigm()
events = events.drop(columns=['trial_type'])
with pytest.warns(UserWarning, match="'trial_type' column not found"):
    events_copy = check_events(events)
assert len(np.unique(events_copy['trial_type'])) == 1
assert events_copy['trial_type'][0] == 'dummy'
events['foo'] = np.zeros(len(events))
with pytest.warns(UserWarning, match='The following unexpected columns in events data will be ignored: foo'):
    events_copy2 = check_events(events)
assert_array_equal(events_copy['trial_type'], events_copy2['trial_type'])
assert_array_equal(events_copy['onset'], events_copy2['onset'])
assert_array_equal(events_copy['duration'], events_copy2['duration'])
assert_array_equal(events_copy['modulation'], events_copy2['modulation'])
```

## Next Steps


---

*Source: test_paradigm.py:82 | Complexity: Advanced | Last updated: 2026-05-18*