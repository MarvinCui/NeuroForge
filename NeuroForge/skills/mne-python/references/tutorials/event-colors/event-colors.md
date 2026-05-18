# How To: Event Colors

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test color assignment.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.chpi`
- `mne.datasets`
- `mne.filter`
- `mne.io`
- `mne.minimum_norm`
- `mne.time_frequency`
- `mne.utils`
- `mne.viz`
- `mne.viz.misc`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test color assignment.'

```python
'Test color assignment.'
```

**Verification:**
```python
assert colors[1] == default_colors[0]
```

### Step 2: Assign events = pick_events(...)

```python
events = pick_events(_get_events(), include=[1, 2])
```

**Verification:**
```python
assert colors[1] == 'k'
```

### Step 3: Assign unique_events = set(...)

```python
unique_events = set(events[:, 2])
```

**Verification:**
```python
assert colors[2] == '#facade'
```

### Step 4: Assign colors = _handle_event_colors(...)

```python
colors = _handle_event_colors(None, unique_events, dict())
```

### Step 5: Assign default_colors = _get_color_list(...)

```python
default_colors = _get_color_list()
```

**Verification:**
```python
assert colors[1] == default_colors[0]
```

### Step 6: Assign colors = _handle_event_colors(...)

```python
colors = _handle_event_colors(color_dict=dict(foo='k', bar='#facade'), unique_events=unique_events, event_id=dict(foo=1, bar=2))
```

**Verification:**
```python
assert colors[1] == 'k'
```


## Complete Example

```python
# Workflow
'Test color assignment.'
events = pick_events(_get_events(), include=[1, 2])
unique_events = set(events[:, 2])
colors = _handle_event_colors(None, unique_events, dict())
default_colors = _get_color_list()
assert colors[1] == default_colors[0]
colors = _handle_event_colors(color_dict=dict(foo='k', bar='#facade'), unique_events=unique_events, event_id=dict(foo=1, bar=2))
assert colors[1] == 'k'
assert colors[2] == '#facade'
```

## Next Steps


---

*Source: test_misc.py:183 | Complexity: Intermediate | Last updated: 2026-05-18*