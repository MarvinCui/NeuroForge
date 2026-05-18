# How To: Rect

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rect

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

### Step 2: Assign rect = visual.Rect(...)

```python
rect = visual.Rect(win)
```

### Step 3: Call rect.draw()

```python
rect.draw()
```

### Step 4: Assign rect.lineColor = 'blue'

```python
rect.lineColor = 'blue'
```

### Step 5: Assign rect.pos = value

```python
rect.pos = [1, 1]
```

### Step 6: Assign rect.ori = 30

```python
rect.ori = 30
```

### Step 7: Assign rect.fillColor = 'pink'

```python
rect.fillColor = 'pink'
```

### Step 8: Call rect.draw()

```python
rect.draw()
```

### Step 9: Call unknown.format()

```python
'{}'.format(rect)
```

### Step 10: Assign rect.width = 1

```python
rect.width = 1
```

### Step 11: Assign rect.height = 1

```python
rect.height = 1
```


## Complete Example

```python
# Workflow
win = self.win
rect = visual.Rect(win)
rect.draw()
rect.lineColor = 'blue'
rect.pos = [1, 1]
rect.ori = 30
rect.fillColor = 'pink'
rect.draw()
'{}'.format(rect)
rect.width = 1
rect.height = 1
```

## Next Steps


---

*Source: test_all_stimuli.py:281 | Complexity: Advanced | Last updated: 2026-05-18*