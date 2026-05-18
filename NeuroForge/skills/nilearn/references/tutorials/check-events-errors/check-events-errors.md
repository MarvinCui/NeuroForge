# How To: Check Events Errors

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

### Step 2: Assign events = basic_paradigm(...)

```python
events = basic_paradigm()
```

### Step 3: Assign missing_onset = events.drop(...)

```python
missing_onset = events.drop(columns=['onset'])
```

### Step 4: Assign missing_duration = events.drop(...)

```python
missing_duration = events.drop(columns=['duration'])
```

### Step 5: Assign wrong_duration = events.copy(...)

```python
wrong_duration = events.copy()
```

### Step 6: Assign unknown = 'foo'

```python
wrong_duration['duration'] = 'foo'
```

### Step 7: Call check_events()

```python
check_events([])
```

### Step 8: Call check_events()

```python
check_events(missing_onset)
```

### Step 9: Call check_events()

```python
check_events(missing_duration)
```

### Step 10: Call check_events()

```python
check_events(wrong_duration)
```


## Complete Example

```python
# Workflow
'Test the function which tests that the events        data describes a valid experimental paradigm.\n    '
events = basic_paradigm()
with pytest.raises(TypeError, match='must be of type'):
    check_events([])
missing_onset = events.drop(columns=['onset'])
with pytest.raises(ValueError, match='The provided events data has no onset column.'):
    check_events(missing_onset)
missing_duration = events.drop(columns=['duration'])
with pytest.raises(ValueError, match='The provided events data has no duration column.'):
    check_events(missing_duration)
wrong_duration = events.copy()
wrong_duration['duration'] = 'foo'
with pytest.raises(ValueError, match='Could not cast duration to float'):
    check_events(wrong_duration)
```

## Next Steps


---

*Source: test_paradigm.py:51 | Complexity: Advanced | Last updated: 2026-05-18*