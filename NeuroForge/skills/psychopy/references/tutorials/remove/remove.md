# How To: Remove

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test remove

## Prerequisites

**Required Modules:**
- `pytest`
- `psychopy`
- `psychopy.preferences`
- `psychopy.visual`
- `pyglet.window.key`
- `pytest`


## Step-by-Step Guide

### Step 1: Assign keys = value

```python
keys = ['a', 'b', 'c']
```

### Step 2: Assign modifiers = value

```python
modifiers = ('ctrl',)
```

### Step 3: Assign func = value

```python
func = self._func
```

### Step 4: Assign global_keys = event._GlobalEventKeys(...)

```python
global_keys = event._GlobalEventKeys()
```

### Step 5: [global_keys.add(key=key, modifiers=modifiers, func=func) for key in keys]

```python
[global_keys.add(key=key, modifiers=modifiers, func=func) for key in keys]
```

### Step 6: Call global_keys.remove()

```python
global_keys.remove(keys[0], modifiers)
```

### Step 7: Assign _ = value

```python
_ = global_keys[keys[0], modifiers]
```


## Complete Example

```python
# Workflow
keys = ['a', 'b', 'c']
modifiers = ('ctrl',)
func = self._func
global_keys = event._GlobalEventKeys()
[global_keys.add(key=key, modifiers=modifiers, func=func) for key in keys]
global_keys.remove(keys[0], modifiers)
with pytest.raises(KeyError):
    _ = global_keys[keys[0], modifiers]
```

## Next Steps


---

*Source: test_keyboard_events.py:206 | Complexity: Intermediate | Last updated: 2026-05-18*