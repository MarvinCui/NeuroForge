# How To: Line Overlaps

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test line overlaps

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
assert line.overlaps(circle_1)
```

### Step 2: Assign circle_1 = visual.Circle(...)

```python
circle_1 = visual.Circle(win, radius=0.25, pos=(0, 0))
```

**Verification:**
```python
assert circle_1.overlaps(circle_1)
```

### Step 3: Assign circle_2 = visual.Circle(...)

```python
circle_2 = visual.Circle(win, radius=0.25, pos=(0, -0.5))
```

**Verification:**
```python
assert not line.overlaps(circle_2)
```

### Step 4: Assign line = visual.Line(...)

```python
line = visual.Line(win, start=(-1, -1), end=(1, 1))
```

**Verification:**
```python
assert not circle_2.overlaps(line)
```


## Complete Example

```python
# Workflow
win.units = 'height'
circle_1 = visual.Circle(win, radius=0.25, pos=(0, 0))
circle_2 = visual.Circle(win, radius=0.25, pos=(0, -0.5))
line = visual.Line(win, start=(-1, -1), end=(1, 1))
assert line.overlaps(circle_1)
assert circle_1.overlaps(circle_1)
assert not line.overlaps(circle_2)
assert not circle_2.overlaps(line)
```

## Next Steps


---

*Source: test_contains_overlaps.py:214 | Complexity: Intermediate | Last updated: 2026-05-18*