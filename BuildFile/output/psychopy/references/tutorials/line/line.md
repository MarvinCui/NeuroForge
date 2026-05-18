# How To: Line

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test line

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

### Step 2: Assign line = visual.Line(...)

```python
line = visual.Line(win)
```

### Step 3: Assign line.start = value

```python
line.start = (0, 0)
```

### Step 4: Assign line.end = value

```python
line.end = (0.1, 0.1)
```

### Step 5: Call line.draw()

```python
line.draw()
```

### Step 6: Call win.flip()

```python
win.flip()
```

### Step 7: Call unknown.format()

```python
'{}'.format(line)
```


## Complete Example

```python
# Workflow
win = self.win
line = visual.Line(win)
line.start = (0, 0)
line.end = (0.1, 0.1)
line.draw()
win.flip()
'{}'.format(line)
```

## Next Steps


---

*Source: test_all_stimuli.py:306 | Complexity: Intermediate | Last updated: 2026-05-18*