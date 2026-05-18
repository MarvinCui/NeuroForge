# How To: Circle

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test circle

## Prerequisites

**Required Modules:**
- `sys`
- `os`
- `copy`
- `pathlib`
- `psychopy`
- `psychopy.visual`
- `psychopy.tools.coordinatetools`
- `psychopy.tests`
- `numpy`
- `pytest`
- `shutil`
- `tempfile`
- `psychopy.tests`
- `psychopy.tools`
- `psychopy.visual`


## Step-by-Step Guide

### Step 1: Assign win = value

```python
win = self.win
```

### Step 2: Assign circle = visual.Circle(...)

```python
circle = visual.Circle(win)
```

### Step 3: Assign circle.fillColor = 'red'

```python
circle.fillColor = 'red'
```

### Step 4: Call circle.draw()

```python
circle.draw()
```

### Step 5: Assign circle.lineColor = 'blue'

```python
circle.lineColor = 'blue'
```

### Step 6: Assign circle.fillColor = None

```python
circle.fillColor = None
```

### Step 7: Assign circle.pos = value

```python
circle.pos = [0.5, -0.5]
```

### Step 8: Assign circle.ori = 30

```python
circle.ori = 30
```

### Step 9: Call circle.draw()

```python
circle.draw()
```

### Step 10: Call unknown.format()

```python
'{}'.format(circle)
```


## Complete Example

```python
# Workflow
win = self.win
circle = visual.Circle(win)
circle.fillColor = 'red'
circle.draw()
circle.lineColor = 'blue'
circle.fillColor = None
circle.pos = [0.5, -0.5]
circle.ori = 30
circle.draw()
'{}'.format(circle)
```

## Next Steps


---

*Source: test_all_stimuli.py:294 | Complexity: Advanced | Last updated: 2026-05-18*