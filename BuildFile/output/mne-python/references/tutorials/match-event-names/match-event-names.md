# How To: Match Event Names

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test event name / event group matching.

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

### Step 1: 'Test event name / event group matching.'

```python
'Test event name / event group matching.'
```

**Verification:**
```python
assert matches == expected_matches
```

### Step 2: Assign event_names = value

```python
event_names = ['auditory/left', 'auditory/right', 'visual/left', 'visual/right']
```

**Verification:**
```python
assert matches == expected_matches
```

### Step 3: Assign keys = value

```python
keys = ['auditory', 'left']
```

**Verification:**
```python
assert matches == expected_matches
```

### Step 4: Assign expected_matches = value

```python
expected_matches = ['auditory/left', 'auditory/right', 'visual/left']
```

**Verification:**
```python
assert matches == []
```

### Step 5: Assign matches = match_event_names(...)

```python
matches = match_event_names(event_names=event_names, keys=keys)
```

**Verification:**
```python
assert matches == []
```

### Step 6: Assign keys = value

```python
keys = ['left', 'auditory']
```

### Step 7: Assign matches = match_event_names(...)

```python
matches = match_event_names(event_names=event_names, keys=keys)
```

**Verification:**
```python
assert matches == expected_matches
```

### Step 8: Assign keys = 'left'

```python
keys = 'left'
```

### Step 9: Assign expected_matches = value

```python
expected_matches = ['auditory/left', 'visual/left']
```

### Step 10: Assign matches = match_event_names(...)

```python
matches = match_event_names(event_names=event_names, keys=keys)
```

**Verification:**
```python
assert matches == expected_matches
```

### Step 11: Assign keys = 'laboratory'

```python
keys = 'laboratory'
```

### Step 12: Assign matches = match_event_names(...)

```python
matches = match_event_names(event_names=event_names, keys=keys, on_missing='ignore')
```

**Verification:**
```python
assert matches == []
```

### Step 13: Call match_event_names()

```python
match_event_names(event_names=event_names, keys=keys)
```

### Step 14: Assign matches = match_event_names(...)

```python
matches = match_event_names(event_names=event_names, keys=keys, on_missing='warn')
```

**Verification:**
```python
assert matches == []
```

### Step 15: Call match_event_names()

```python
match_event_names(event_names=event_names, keys=keys)
```


## Complete Example

```python
# Workflow
'Test event name / event group matching.'
event_names = ['auditory/left', 'auditory/right', 'visual/left', 'visual/right']
keys = ['auditory', 'left']
expected_matches = ['auditory/left', 'auditory/right', 'visual/left']
matches = match_event_names(event_names=event_names, keys=keys)
assert matches == expected_matches
keys = ['left', 'auditory']
matches = match_event_names(event_names=event_names, keys=keys)
assert matches == expected_matches
keys = 'left'
expected_matches = ['auditory/left', 'visual/left']
matches = match_event_names(event_names=event_names, keys=keys)
assert matches == expected_matches
for keys in (123, [123, 456]):
    with pytest.raises(ValueError, match='keys must be strings'):
        match_event_names(event_names=event_names, keys=keys)
keys = 'laboratory'
with pytest.raises(KeyError, match='could not be found'):
    match_event_names(event_names=event_names, keys=keys)
with pytest.warns(RuntimeWarning, match='could not be found'):
    matches = match_event_names(event_names=event_names, keys=keys, on_missing='warn')
    assert matches == []
matches = match_event_names(event_names=event_names, keys=keys, on_missing='ignore')
assert matches == []
```

## Next Steps


---

*Source: test_event.py:614 | Complexity: Advanced | Last updated: 2026-05-18*