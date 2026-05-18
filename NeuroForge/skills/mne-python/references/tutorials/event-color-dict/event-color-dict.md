# How To: Event Color Dict

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test handling of event_color.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `cycler`
- `matplotlib`
- `numpy.testing`
- `mne`
- `mne.epochs`
- `mne.event`
- `mne.io`
- `mne.viz`
- `mne.viz.ui_events`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test handling of event_color.'

```python
'Test handling of event_color.'
```

**Verification:**
```python
assert one == two
```

### Step 2: Assign one = _make_event_color_dict(...)

```python
one = _make_event_color_dict('k')
```

**Verification:**
```python
assert one == three
```

### Step 3: Assign two = _make_event_color_dict(...)

```python
two = _make_event_color_dict((0, 0, 0))
```

**Verification:**
```python
assert one == two
```

### Step 4: Assign three = _make_event_color_dict(...)

```python
three = _make_event_color_dict('#000')
```

**Verification:**
```python
assert one[2] == two[2]
```

### Step 5: Assign event_id = dict(...)

```python
event_id = dict(foo=1, bar=2)
```

### Step 6: Assign one = _make_event_color_dict(...)

```python
one = _make_event_color_dict({1: 'r', 2: 'b'}, event_id=event_id)
```

### Step 7: Assign two = _make_event_color_dict(...)

```python
two = _make_event_color_dict(dict(foo='r', bar='b'), event_id=event_id)
```

**Verification:**
```python
assert one == two
```

### Step 8: Assign one = _make_event_color_dict(...)

```python
one = _make_event_color_dict({1: 'r', -1: 'b'}, event_id=event_id)
```

### Step 9: Assign two = _make_event_color_dict(...)

```python
two = _make_event_color_dict({1: 'r', 2: 'b'}, event_id=event_id)
```

**Verification:**
```python
assert one[2] == two[2]
```

### Step 10: Assign _ = _make_event_color_dict(...)

```python
_ = _make_event_color_dict({-2: 'r', -1: 'b'})
```


## Complete Example

```python
# Workflow
'Test handling of event_color.'
one = _make_event_color_dict('k')
two = _make_event_color_dict((0, 0, 0))
three = _make_event_color_dict('#000')
assert one == two
assert one == three
event_id = dict(foo=1, bar=2)
one = _make_event_color_dict({1: 'r', 2: 'b'}, event_id=event_id)
two = _make_event_color_dict(dict(foo='r', bar='b'), event_id=event_id)
assert one == two
one = _make_event_color_dict({1: 'r', -1: 'b'}, event_id=event_id)
two = _make_event_color_dict({1: 'r', 2: 'b'}, event_id=event_id)
assert one[2] == two[2]
with pytest.raises(KeyError, match='must be strictly positive, or -1'):
    _ = _make_event_color_dict({-2: 'r', -1: 'b'})
```

## Next Steps


---

*Source: test_utils.py:186 | Complexity: Advanced | Last updated: 2026-05-18*