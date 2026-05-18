# How To: Horiz

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test horiz

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

### Step 1: Assign exemplars = value

```python
exemplars = [{'size': (1, 0.2), 'ori': 0, 'horiz': True, 'tag': 'horiz'}, {'size': (0.2, 1), 'ori': 0, 'horiz': False, 'tag': 'vert'}, {'size': (1, 0.2), 'ori': 90, 'horiz': False, 'tag': 'vert'}, {'size': (0.2, 1), 'ori': 90, 'horiz': True, 'tag': 'horiz'}]
```

**Verification:**
```python
assert obj.horiz == case['horiz']
```

### Step 2: Assign tykes = value

```python
tykes = [{'size': (1, 0.2), 'ori': 25, 'horiz': True, 'tag': 'accute_horiz'}, {'size': (0.2, 1), 'ori': 25, 'horiz': False, 'tag': 'accute_vert'}, {'size': (1, 0.2), 'ori': 115, 'horiz': False, 'tag': 'obtuse_horiz'}, {'size': (0.2, 1), 'ori': 115, 'horiz': True, 'tag': 'obtuse_vert'}]
```

### Step 3: Call self.win.flip()

```python
self.win.flip()
```

### Step 4: Assign obj = Slider(...)

```python
obj = Slider(self.win, labels=['a', 'b', 'c', 'd'], ticks=[1, 2, 3, 4], labelHeight=0.2, labelColor='red', size=case['size'], ori=case['ori'])
```

**Verification:**
```python
assert obj.horiz == case['horiz']
```

### Step 5: Call obj.draw()

```python
obj.draw()
```

### Step 6: Assign filename = value

```python
filename = f"test_slider_horiz_{case['tag']}.png"
```

### Step 7: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=10)
```

### Step 8: Call self.win.flip()

```python
self.win.flip()
```


## Complete Example

```python
# Workflow
exemplars = [{'size': (1, 0.2), 'ori': 0, 'horiz': True, 'tag': 'horiz'}, {'size': (0.2, 1), 'ori': 0, 'horiz': False, 'tag': 'vert'}, {'size': (1, 0.2), 'ori': 90, 'horiz': False, 'tag': 'vert'}, {'size': (0.2, 1), 'ori': 90, 'horiz': True, 'tag': 'horiz'}]
tykes = [{'size': (1, 0.2), 'ori': 25, 'horiz': True, 'tag': 'accute_horiz'}, {'size': (0.2, 1), 'ori': 25, 'horiz': False, 'tag': 'accute_vert'}, {'size': (1, 0.2), 'ori': 115, 'horiz': False, 'tag': 'obtuse_horiz'}, {'size': (0.2, 1), 'ori': 115, 'horiz': True, 'tag': 'obtuse_vert'}]
self.win.flip()
for case in exemplars + tykes:
    obj = Slider(self.win, labels=['a', 'b', 'c', 'd'], ticks=[1, 2, 3, 4], labelHeight=0.2, labelColor='red', size=case['size'], ori=case['ori'])
    assert obj.horiz == case['horiz']
    obj.draw()
    filename = f"test_slider_horiz_{case['tag']}.png"
    utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=10)
    self.win.flip()
```

## Next Steps


---

*Source: test_slider.py:45 | Complexity: Advanced | Last updated: 2026-05-18*