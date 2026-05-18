# How To: Add Args And Kwargs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test add args and kwargs

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
assert global_keys[key, ()].func_args == args
```

### Step 2: Assign func = value

```python
func = self._func
```

**Verification:**
```python
assert global_keys[key, ()].func_kwargs == kwargs
```

### Step 3: Assign args = value

```python
args = (1, 2, 3)
```

### Step 4: Assign kwargs = dict(...)

```python
kwargs = dict(foo=1, bar=2)
```

### Step 5: Assign global_keys = event._GlobalEventKeys(...)

```python
global_keys = event._GlobalEventKeys()
```

### Step 6: Call global_keys.add()

```python
global_keys.add(key=key, func=func, func_args=args, func_kwargs=kwargs)
```

**Verification:**
```python
assert global_keys[key, ()].func_args == args
```


## Complete Example

```python
# Workflow
key = 'a'
func = self._func
args = (1, 2, 3)
kwargs = dict(foo=1, bar=2)
global_keys = event._GlobalEventKeys()
global_keys.add(key=key, func=func, func_args=args, func_kwargs=kwargs)
assert global_keys[key, ()].func_args == args
assert global_keys[key, ()].func_kwargs == kwargs
```

## Next Steps


---

*Source: test_keyboard_events.py:176 | Complexity: Intermediate | Last updated: 2026-05-18*