# How To: Set Visible

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test set visible

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

### Step 2: Call pytest.skip()

```python
pytest.skip()
```

### Step 3: Call m.setVisible()

```python
m.setVisible(v)
```

### Step 4: Assign w = value

```python
w = self.win
```

### Step 5: Assign m.win = None

```python
m.win = None
```

### Step 6: Call m.setVisible()

```python
m.setVisible(v)
```

### Step 7: Assign m.win = w

```python
m.win = w
```


## Complete Example

```python
# Workflow
if self.win.winType == 'pygame':
    pytest.skip()
m = event.Mouse()
for v in (0, 1):
    m.setVisible(v)
    w = self.win
    m.win = None
    m.setVisible(v)
    m.win = w
```

## Next Steps


---

*Source: test_event.py:239 | Complexity: Intermediate | Last updated: 2026-05-18*