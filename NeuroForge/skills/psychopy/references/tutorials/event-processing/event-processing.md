# How To: Event Processing

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test event processing

## Prerequisites

**Required Modules:**
- `pytest`
- `psychopy`
- `psychopy.preferences`
- `psychopy.visual`
- `pyglet.window.key`
- `pytest`


## Step-by-Step Guide

### Step 1: Assign key = 'a'

```python
key = 'a'
```

**Verification:**
```python
assert r[0] == args
```

### Step 2: Assign modifiers = 0

```python
modifiers = 0
```

**Verification:**
```python
assert r[1] == kwargs
```

### Step 3: Assign func = value

```python
func = self._func
```

### Step 4: Assign args = value

```python
args = (1, 2, 3)
```

### Step 5: Assign kwargs = dict(...)

```python
kwargs = dict(foo=1, bar=2)
```

### Step 6: Call event.globalKeys.add()

```python
event.globalKeys.add(key=key, func=func, func_args=args, func_kwargs=kwargs)
```

### Step 7: Assign r = event._process_global_event_key(...)

```python
r = event._process_global_event_key(key, modifiers)
```

**Verification:**
```python
assert r[0] == args
```


## Complete Example

```python
# Workflow
key = 'a'
modifiers = 0
func = self._func
args = (1, 2, 3)
kwargs = dict(foo=1, bar=2)
event.globalKeys.add(key=key, func=func, func_args=args, func_kwargs=kwargs)
r = event._process_global_event_key(key, modifiers)
assert r[0] == args
assert r[1] == kwargs
```

## Next Steps


---

*Source: test_keyboard_events.py:323 | Complexity: Intermediate | Last updated: 2026-05-18*