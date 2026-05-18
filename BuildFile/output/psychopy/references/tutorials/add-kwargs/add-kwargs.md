# How To: Add Kwargs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test add kwargs

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
assert global_keys[key, ()].func_kwargs == kwargs
```

### Step 2: Assign func = value

```python
func = self._func
```

### Step 3: Assign kwargs = dict(...)

```python
kwargs = dict(foo=1, bar=2)
```

### Step 4: Assign global_keys = event._GlobalEventKeys(...)

```python
global_keys = event._GlobalEventKeys()
```

### Step 5: Call global_keys.add()

```python
global_keys.add(key=key, func=func, func_kwargs=kwargs)
```

**Verification:**
```python
assert global_keys[key, ()].func_kwargs == kwargs
```


## Complete Example

```python
# Workflow
key = 'a'
func = self._func
kwargs = dict(foo=1, bar=2)
global_keys = event._GlobalEventKeys()
global_keys.add(key=key, func=func, func_kwargs=kwargs)
assert global_keys[key, ()].func_kwargs == kwargs
```

## Next Steps


---

*Source: test_keyboard_events.py:166 | Complexity: Intermediate | Last updated: 2026-05-18*