# How To: Len

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test len

## Prerequisites

**Required Modules:**
- `pytest`
- `psychopy`
- `psychopy.preferences`
- `psychopy.visual`
- `pyglet.window.key`
- `pytest`


## Step-by-Step Guide

### Step 1: Assign unknown = ''

```python
prefs.general['shutdownKey'] = ''
```

**Verification:**
```python
assert len(global_keys) == 0
```

### Step 2: Assign key = 'escape'

```python
key = 'escape'
```

**Verification:**
```python
assert len(global_keys) == 1
```

### Step 3: Assign func = value

```python
func = self._func
```

**Verification:**
```python
assert len(global_keys) == 0
```

### Step 4: Assign global_keys = event._GlobalEventKeys(...)

```python
global_keys = event._GlobalEventKeys()
```

**Verification:**
```python
assert len(global_keys) == 0
```

### Step 5: Call global_keys.add()

```python
global_keys.add(key=key, func=func)
```

**Verification:**
```python
assert len(global_keys) == 1
```


## Complete Example

```python
# Workflow
prefs.general['shutdownKey'] = ''
key = 'escape'
func = self._func
global_keys = event._GlobalEventKeys()
assert len(global_keys) == 0
global_keys.add(key=key, func=func)
assert len(global_keys) == 1
del global_keys[key, ()]
assert len(global_keys) == 0
```

## Next Steps


---

*Source: test_keyboard_events.py:309 | Complexity: Intermediate | Last updated: 2026-05-18*