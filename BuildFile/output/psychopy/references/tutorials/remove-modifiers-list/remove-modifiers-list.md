# How To: Remove Modifiers List

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test remove modifiers list

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

### Step 6: Call global_keys.remove()

```python
global_keys.remove(key, modifiers)
```

### Step 7: Assign _ = value

```python
_ = global_keys[key, modifiers]
```


## Complete Example

```python
# Workflow
key = 'a'
modifiers = ['ctrl', 'alt']
func = self._func
global_keys = event._GlobalEventKeys()
global_keys.add(key=key, modifiers=modifiers, func=func)
global_keys.remove(key, modifiers)
with pytest.raises(KeyError):
    _ = global_keys[key, modifiers]
```

## Next Steps


---

*Source: test_keyboard_events.py:219 | Complexity: Intermediate | Last updated: 2026-05-18*