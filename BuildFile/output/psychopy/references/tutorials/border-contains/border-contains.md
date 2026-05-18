# How To: Border Contains

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test border contains

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
assert s.contains(p)
```

### Step 2: Assign thingVert = value

```python
thingVert = [(0, 0), (0, 0.4), (0.4, 0.4), (0.4, 0), (0.1, 0), (0.1, 0.1), (0.3, 0.1), (0.3, 0.3), (0.1, 0.3), (0.1, 0), (0, 0), (0.1, -0.1), (0.3, -0.1), (0.3, -0.3), (0.1, -0.3), (0.1, -0.1)]
```

**Verification:**
```python
assert not s.contains(p)
```

### Step 3: Assign inside_pts = value

```python
inside_pts = [(0.05, 0.05), (0.15, -0.15)]
```

**Verification:**
```python
assert s.contains(p), 'no .border property (falls through to relying on tesselated .vertices)'
```

### Step 4: Assign outside_pts = value

```python
outside_pts = [(-0.2, 0)]
```

**Verification:**
```python
assert not s.contains(p)
```

### Step 5: Assign hole_pts = value

```python
hole_pts = [(0.2, 0.2)]
```

**Verification:**
```python
assert not s.contains(p)
```

### Step 6: Assign s = visual.ShapeStim(...)

```python
s = visual.ShapeStim(win, vertices=thingVert, fillColor='blue', lineWidth=1, lineColor='white')
```

### Step 7: Call s.draw()

```python
s.draw()
```

### Step 8: Call win.flip()

```python
win.flip()
```

### Step 9: Assign s.border = thingVert

```python
s.border = thingVert
```

**Verification:**
```python
assert s.contains(p)
```


## Complete Example

```python
# Workflow
win.units = 'height'
thingVert = [(0, 0), (0, 0.4), (0.4, 0.4), (0.4, 0), (0.1, 0), (0.1, 0.1), (0.3, 0.1), (0.3, 0.3), (0.1, 0.3), (0.1, 0), (0, 0), (0.1, -0.1), (0.3, -0.1), (0.3, -0.3), (0.1, -0.3), (0.1, -0.1)]
inside_pts = [(0.05, 0.05), (0.15, -0.15)]
outside_pts = [(-0.2, 0)]
hole_pts = [(0.2, 0.2)]
s = visual.ShapeStim(win, vertices=thingVert, fillColor='blue', lineWidth=1, lineColor='white')
s.draw()
win.flip()
for p in inside_pts:
    assert s.contains(p)
for p in outside_pts + hole_pts:
    assert not s.contains(p)
del s.border
for p in hole_pts:
    assert s.contains(p), 'no .border property (falls through to relying on tesselated .vertices)'
for p in outside_pts:
    assert not s.contains(p)
s.border = thingVert
for p in hole_pts:
    assert not s.contains(p)
```

## Next Steps


---

*Source: test_contains_overlaps.py:180 | Complexity: Advanced | Last updated: 2026-05-18*