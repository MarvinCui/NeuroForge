# How To: Mouse Clock

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mouse clock

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

### Step 1: Assign unknown = value

```python
x, y = (0, 0)
```

**Verification:**
```python
assert event.mouseButtons != zeros
```

### Step 2: Assign unknown = value

```python
scroll_x, scroll_y = (1, 1)
```

**Verification:**
```python
assert event.mouseTimes != zeros
```

### Step 3: Assign unknown = value

```python
dx, dy = (1, 1)
```

**Verification:**
```python
assert event.mouseButtons == zeros
```

### Step 4: Assign zeros = value

```python
zeros = [0, 0, 0]
```

**Verification:**
```python
assert m.mouseMoveTime() >= 0
```

### Step 5: Call event._onPygletMouseWheel()

```python
event._onPygletMouseWheel(x, y, scroll_x, scroll_y)
```

**Verification:**
```python
assert t - 0.01 < m.mouseMoveTime() < t + 0.01
```

### Step 6: Call event._onPygletMouseMotion()

```python
event._onPygletMouseMotion(x, y, dx, dy)
```

### Step 7: Call event.startMoveClock()

```python
event.startMoveClock()
```

### Step 8: Call event.stopMoveClock()

```python
event.stopMoveClock()
```

### Step 9: Call event.resetMoveClock()

```python
event.resetMoveClock()
```

### Step 10: Assign m = event.Mouse(...)

```python
m = event.Mouse()
```

**Verification:**
```python
assert m.mouseMoveTime() >= 0
```

### Step 11: Assign t = 0.05

```python
t = 0.05
```

### Step 12: Call core.wait()

```python
core.wait(t)
```

**Verification:**
```python
assert t - 0.01 < m.mouseMoveTime() < t + 0.01
```

### Step 13: Assign event.mouseButtons = copy.copy(...)

```python
event.mouseButtons = copy.copy(zeros)
```

### Step 14: Assign event.mouseTimes = copy.copy(...)

```python
event.mouseTimes = copy.copy(zeros)
```

### Step 15: Call event._onPygletMousePress()

```python
event._onPygletMousePress(x, y, b, None)
```

**Verification:**
```python
assert event.mouseButtons != zeros
```

### Step 16: Call event._onPygletMouseRelease()

```python
event._onPygletMouseRelease(x, y, b, None)
```

**Verification:**
```python
assert event.mouseButtons == zeros
```


## Complete Example

```python
# Workflow
x, y = (0, 0)
scroll_x, scroll_y = (1, 1)
dx, dy = (1, 1)
zeros = [0, 0, 0]
for b in [pyglet.window.mouse.LEFT, pyglet.window.mouse.MIDDLE, pyglet.window.mouse.RIGHT]:
    event.mouseButtons = copy.copy(zeros)
    event.mouseTimes = copy.copy(zeros)
    event._onPygletMousePress(x, y, b, None)
    assert event.mouseButtons != zeros
    assert event.mouseTimes != zeros
    event._onPygletMouseRelease(x, y, b, None)
    assert event.mouseButtons == zeros
event._onPygletMouseWheel(x, y, scroll_x, scroll_y)
event._onPygletMouseMotion(x, y, dx, dy)
event.startMoveClock()
event.stopMoveClock()
event.resetMoveClock()
m = event.Mouse()
assert m.mouseMoveTime() >= 0
t = 0.05
core.wait(t)
assert t - 0.01 < m.mouseMoveTime() < t + 0.01
```

## Next Steps


---

*Source: test_event.py:99 | Complexity: Advanced | Last updated: 2026-05-18*