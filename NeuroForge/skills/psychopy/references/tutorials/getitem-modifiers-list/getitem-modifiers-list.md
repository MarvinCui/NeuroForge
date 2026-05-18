# How To: Getitem Modifiers List

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test getitem modifiers list

## Prerequisites

**Required Modules:**
- `pytest`
- `psychopy`
- `psychopy.preferences`
- `psychopy.visual`
- `pyglet.window.key`
- `pytest`


## Step-by-Step Guide

### Step 1: Assign key = 'escape'

```python
key = 'escape'
```

**Verification:**
```python
assert global_keys[key, modifiers] == global_keys._events[key, tuple(modifiers)]
```

### Step 2: Assign modifiers = value

```python
modifiers = ['ctrl', 'alt']
```

### Step 3: Assign func = value

```python
func = self._func
```

### Step 4: Assign global_keys = event._GlobalEventKeys(...)

```python
global_keys = event._GlobalEventKeys()
```

### Step 5: Call global_keys.add()

```python
global_keys.add(key=key, modifiers=modifiers, func=func)
```

**Verification:**
```python
assert global_keys[key, modifiers] == global_keys._events[key, tuple(modifiers)]
```


## Complete Example

```python
# Workflow
key = 'escape'
modifiers = ['ctrl', 'alt']
func = self._func
global_keys = event._GlobalEventKeys()
global_keys.add(key=key, modifiers=modifiers, func=func)
assert global_keys[key, modifiers] == global_keys._events[key, tuple(modifiers)]
```

## Next Steps


---

*Source: test_keyboard_events.py:267 | Complexity: Intermediate | Last updated: 2026-05-18*