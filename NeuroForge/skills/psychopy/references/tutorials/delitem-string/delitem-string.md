# How To: Delitem String

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test delitem string

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

### Step 2: Assign func = value

```python
func = self._func
```

### Step 3: Assign global_keys = event._GlobalEventKeys(...)

```python
global_keys = event._GlobalEventKeys()
```

### Step 4: Call global_keys.add()

```python
global_keys.add(key=key, func=func)
```

### Step 5: Assign _ = value

```python
_ = global_keys[key]
```


## Complete Example

```python
# Workflow
key = 'escape'
func = self._func
global_keys = event._GlobalEventKeys()
global_keys.add(key=key, func=func)
del global_keys[key]
with pytest.raises(KeyError):
    _ = global_keys[key]
```

## Next Steps


---

*Source: test_keyboard_events.py:298 | Complexity: Intermediate | Last updated: 2026-05-18*