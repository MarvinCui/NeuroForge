# How To: Check Events

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check events

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

### Step 1: Assign events = basic_paradigm(...)

```python
events = basic_paradigm()
```

**Verification:**
```python
assert_array_equal(events_copy['trial_type'], ['c0', 'c0', 'c0', 'c1', 'c1', 'c1', 'c2', 'c2', 'c2'])
```

### Step 2: Assign events_copy = check_events(...)

```python
events_copy = check_events(events)
```

**Verification:**
```python
assert_array_equal(events_copy['modulation'], np.ones(len(events)))
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(events_copy['trial_type'], ['c0', 'c0', 'c0', 'c1', 'c1', 'c1', 'c2', 'c2', 'c2'])
```

**Verification:**
```python
assert_array_equal(events_copy['modulation'], events['modulation'])
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(events_copy['modulation'], np.ones(len(events)))
```

### Step 5: Assign unknown = np.ones(...)

```python
events['modulation'] = np.ones(len(events))
```

### Step 6: Assign events_copy = check_events(...)

```python
events_copy = check_events(events)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(events_copy['modulation'], events['modulation'])
```


## Complete Example

```python
# Workflow
events = basic_paradigm()
events_copy = check_events(events)
assert_array_equal(events_copy['trial_type'], ['c0', 'c0', 'c0', 'c1', 'c1', 'c1', 'c2', 'c2', 'c2'])
assert_array_equal(events_copy['modulation'], np.ones(len(events)))
events['modulation'] = np.ones(len(events))
events_copy = check_events(events)
assert_array_equal(events_copy['modulation'], events['modulation'])
```

## Next Steps


---

*Source: test_paradigm.py:32 | Complexity: Intermediate | Last updated: 2026-05-18*