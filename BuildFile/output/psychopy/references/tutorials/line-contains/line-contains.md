# How To: Line Contains

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test line contains

## Prerequisites

**Required Modules:**
- `pathlib`
- `psychopy`
- `psychopy.tests`
- `psychopy.visual`
- `numpy`
- `matplotlib`
- `matplotlib`


## Step-by-Step Guide

### Step 1: Assign win.units = 'height'

```python
win.units = 'height'
```

**Verification:**
```python
assert line.contains(point_1) is False
```

### Step 2: Assign point_1 = value

```python
point_1 = (0, 0)
```

**Verification:**
```python
assert line.contains(point_2) is False
```

### Step 3: Assign point_2 = value

```python
point_2 = (0, -0.5)
```

### Step 4: Assign line = visual.Line(...)

```python
line = visual.Line(win, start=(-1, -1), end=(1, 1))
```

**Verification:**
```python
assert line.contains(point_1) is False
```


## Complete Example

```python
# Workflow
win.units = 'height'
point_1 = (0, 0)
point_2 = (0, -0.5)
line = visual.Line(win, start=(-1, -1), end=(1, 1))
assert line.contains(point_1) is False
assert line.contains(point_2) is False
```

## Next Steps


---

*Source: test_contains_overlaps.py:227 | Complexity: Intermediate | Last updated: 2026-05-18*