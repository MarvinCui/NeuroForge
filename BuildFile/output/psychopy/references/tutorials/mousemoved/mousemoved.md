# How To: Mousemoved

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mouseMoved

## Prerequisites

**Required Modules:**
- `psychopy.visual`
- `psychopy`
- `psychopy.constants`
- `pyglet`
- `pyglet.window.mouse`
- `pytest`
- `copy`
- `threading`
- `numpy`
- `psychopy.tests`
- `pygame`
- `pytest`


## Step-by-Step Guide

### Step 1: Assign m = event.Mouse(...)

```python
m = event.Mouse()
```

**Verification:**
```python
assert m.mouseMoved()
```

### Step 2: Assign m.prevPos = value

```python
m.prevPos = [0, 0]
```

**Verification:**
```python
assert m.mouseMoved(distance=0.5)
```

### Step 3: Assign m.lastPos = value

```python
m.lastPos = [0, 1]
```

**Verification:**
```python
assert not m.mouseMoved(reset=reset)
```

### Step 4: Assign m.prevPos = value

```python
m.prevPos = [0, 0]
```

### Step 5: Assign m.lastPos = value

```python
m.lastPos = [0, 1]
```

**Verification:**
```python
assert m.mouseMoved(distance=0.5)
```


## Complete Example

```python
# Workflow
m = event.Mouse()
m.prevPos = [0, 0]
m.lastPos = [0, 1]
assert m.mouseMoved()
m.prevPos = [0, 0]
m.lastPos = [0, 1]
assert m.mouseMoved(distance=0.5)
for reset in [True, 'here', (1, 2)]:
    assert not m.mouseMoved(reset=reset)
```

## Next Steps


---

*Source: test_event.py:227 | Complexity: Intermediate | Last updated: 2026-05-18*