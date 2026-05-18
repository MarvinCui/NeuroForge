# How To: Fps

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that images can be updated sufficiently fast to create frame animations

## Prerequisites

**Required Modules:**
- `pathlib`
- `psychopy`
- `test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.tests`
- `pytest`


## Step-by-Step Guide

### Step 1: '\n        Check that images can be updated sufficiently fast to create frame animations\n        '

```python
'\n        Check that images can be updated sufficiently fast to create frame animations\n        '
```

**Verification:**
```python
assert fps > case['fps'], f"Max frame rate for {size}x{size} animations should be at least {case['fps']}, but was {fps}"
```

### Step 2: Assign clock = core.Clock(...)

```python
clock = core.Clock()
```

### Step 3: Call pytest.skip()

```python
pytest.skip()
```

### Step 4: Assign size = value

```python
size = case['size']
```

### Step 5: Assign win = visual.Window(...)

```python
win = visual.Window(size=(size, size))
```

### Step 6: Assign img = visual.ImageStim(...)

```python
img = visual.ImageStim(win, units='pix', size=(size, size))
```

### Step 7: Assign refr = value

```python
refr = []
```

### Step 8: Assign fps = round(...)

```python
fps = round(1 / max(refr))
```

**Verification:**
```python
assert fps > case['fps'], f"Max frame rate for {size}x{size} animations should be at least {case['fps']}, but was {fps}"
```

### Step 9: Call win.close()

```python
win.close()
```

### Step 10: Call clock.reset()

```python
clock.reset()
```

### Step 11: Assign img.image = frame

```python
img.image = frame
```

### Step 12: Call img.draw()

```python
img.draw()
```

### Step 13: Call win.flip()

```python
win.flip()
```

### Step 14: Call refr.append()

```python
refr.append(clock.getTime())
```


## Complete Example

```python
# Workflow
'\n        Check that images can be updated sufficiently fast to create frame animations\n        '
if utils.RUNNING_IN_VM:
    pytest.skip()
clock = core.Clock()
for case in self.cases:
    size = case['size']
    win = visual.Window(size=(size, size))
    img = visual.ImageStim(win, units='pix', size=(size, size))
    refr = []
    for frame in case['frames']:
        clock.reset()
        img.image = frame
        img.draw()
        win.flip()
        refr.append(clock.getTime())
    fps = round(1 / max(refr))
    assert fps > case['fps'], f"Max frame rate for {size}x{size} animations should be at least {case['fps']}, but was {fps}"
    win.close()
    del img
```

## Next Steps


---

*Source: test_image.py:184 | Complexity: Advanced | Last updated: 2026-05-18*