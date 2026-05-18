# How To: Add Invalid Modifiers

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test add invalid modifiers

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

### Step 2: Assign modifiers = value

```python
modifiers = ('foo', 'bar')
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


## Complete Example

```python
# Workflow
key = 'a'
modifiers = ('foo', 'bar')
func = self._func
global_keys = event._GlobalEventKeys()
with pytest.raises(ValueError):
    global_keys.add(key=key, modifiers=modifiers, func=func)
```

## Next Steps


---

*Source: test_keyboard_events.py:197 | Complexity: Intermediate | Last updated: 2026-05-18*