# How To: Triangle Marker

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test triangle marker

## Prerequisites

**Required Modules:**
- `pathlib`
- `psychopy.tests`
- `psychopy.tests.test_visual.test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.visual.window`
- `psychopy.visual.slider`
- `psychopy.visual.elementarray`
- `psychopy.visual.shape`
- `psychopy.visual.rect`
- `psychopy`
- `numpy`
- `random`


## Step-by-Step Guide

### Step 1: Assign cases = value

```python
cases = [{'horiz': True, 'flip': True}, {'horiz': True, 'flip': False}, {'horiz': False, 'flip': True}, {'horiz': False, 'flip': False}]
```

### Step 2: Assign s = Slider(...)

```python
s = Slider(self.win, units='height', pos=(0, 0), ticks=(0, 1, 2), styleTweaks=['triangleMarker'])
```

### Step 3: Assign s.rating = 1

```python
s.rating = 1
```

### Step 4: Assign s.flip = value

```python
s.flip = case['flip']
```

### Step 5: Call s.draw()

```python
s.draw()
```

### Step 6: Assign filename = value

```python
filename = 'test_slider_triangle_horiz_%(horiz)s_flip_%(flip)s.png' % case
```

### Step 7: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win)
```

### Step 8: Call self.win.flip()

```python
self.win.flip()
```

### Step 9: Assign s.size = value

```python
s.size = (1, 0.1)
```

### Step 10: Assign s.size = value

```python
s.size = (0.1, 1)
```


## Complete Example

```python
# Workflow
cases = [{'horiz': True, 'flip': True}, {'horiz': True, 'flip': False}, {'horiz': False, 'flip': True}, {'horiz': False, 'flip': False}]
s = Slider(self.win, units='height', pos=(0, 0), ticks=(0, 1, 2), styleTweaks=['triangleMarker'])
s.rating = 1
for case in cases:
    if case['horiz']:
        s.size = (1, 0.1)
    else:
        s.size = (0.1, 1)
    s.flip = case['flip']
    s.draw()
    filename = 'test_slider_triangle_horiz_%(horiz)s_flip_%(flip)s.png' % case
    utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win)
    self.win.flip()
```

## Next Steps


---

*Source: test_slider.py:124 | Complexity: Advanced | Last updated: 2026-05-18*