# How To: Tick And Label Locs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test tick and label locs

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
exemplars = [{'ticks': [1, 2, 3, 4, 5], 'labels': ['a', 'b', 'c', 'd', 'e'], 'tag': 'simple'}, {'ticks': [1, 2, 3, 9, 10], 'labels': ['a', 'b', 'c', 'd', 'e'], 'tag': 'clustered'}, {'ticks': [1, 2, 3, 4, 5], 'labels': ['', 'b', 'c', 'd', ''], 'tag': 'blanks'}, {'ticks': None, 'labels': ['a', 'b', 'c', 'd', 'e'], 'tag': 'noticks'}, {'ticks': [1, 2, 3, 4, 5], 'labels': None, 'tag': 'nolabels'}]
```

### Step 2: Assign tykes = value

```python
tykes = [{'ticks': [1, 2, 3], 'labels': ['a', 'b', 'c', 'd', 'e'], 'tag': 'morelabels'}, {'ticks': [1, 2, 3, 4, 5], 'labels': ['a', 'b', 'c'], 'tag': 'moreticks'}, {'ticks': [1, 9, 10], 'labels': ['a', 'b', 'c', 'd', 'e'], 'tag': 'morelabelsclustered'}, {'ticks': [1, 7, 8, 9, 10], 'labels': ['a', 'b', 'c', 'd'], 'tag': 'moreticksclustered'}]
```

### Step 3: Call self.win.flip()

```python
self.win.flip()
```

### Step 4: Assign vert = Slider(...)

```python
vert = Slider(self.win, size=(0.1, 0.5), pos=(-0.25, 0), units='height', labels=case['labels'], ticks=case['ticks'])
```

### Step 5: Call vert.draw()

```python
vert.draw()
```

### Step 6: Assign horiz = Slider(...)

```python
horiz = Slider(self.win, size=(0.5, 0.1), pos=(0.2, 0), units='height', labels=case['labels'], ticks=case['ticks'])
```

### Step 7: Call horiz.draw()

```python
horiz.draw()
```

### Step 8: Assign filename = value

```python
filename = 'test_slider_ticklabelloc_%(tag)s.png' % case
```

### Step 9: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win)
```

### Step 10: Call self.win.flip()

```python
self.win.flip()
```


## Complete Example

```python
# Workflow
exemplars = [{'ticks': [1, 2, 3, 4, 5], 'labels': ['a', 'b', 'c', 'd', 'e'], 'tag': 'simple'}, {'ticks': [1, 2, 3, 9, 10], 'labels': ['a', 'b', 'c', 'd', 'e'], 'tag': 'clustered'}, {'ticks': [1, 2, 3, 4, 5], 'labels': ['', 'b', 'c', 'd', ''], 'tag': 'blanks'}, {'ticks': None, 'labels': ['a', 'b', 'c', 'd', 'e'], 'tag': 'noticks'}, {'ticks': [1, 2, 3, 4, 5], 'labels': None, 'tag': 'nolabels'}]
tykes = [{'ticks': [1, 2, 3], 'labels': ['a', 'b', 'c', 'd', 'e'], 'tag': 'morelabels'}, {'ticks': [1, 2, 3, 4, 5], 'labels': ['a', 'b', 'c'], 'tag': 'moreticks'}, {'ticks': [1, 9, 10], 'labels': ['a', 'b', 'c', 'd', 'e'], 'tag': 'morelabelsclustered'}, {'ticks': [1, 7, 8, 9, 10], 'labels': ['a', 'b', 'c', 'd'], 'tag': 'moreticksclustered'}]
self.win.flip()
for case in exemplars + tykes:
    vert = Slider(self.win, size=(0.1, 0.5), pos=(-0.25, 0), units='height', labels=case['labels'], ticks=case['ticks'])
    vert.draw()
    horiz = Slider(self.win, size=(0.5, 0.1), pos=(0.2, 0), units='height', labels=case['labels'], ticks=case['ticks'])
    horiz.draw()
    filename = 'test_slider_ticklabelloc_%(tag)s.png' % case
    utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win)
    self.win.flip()
```

## Next Steps


---

*Source: test_slider.py:175 | Complexity: Advanced | Last updated: 2026-05-18*