# How To: Ori

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test ori

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `psychopy`
- `psychopy.alerts`
- `psychopy.alerts._errorHandler`
- `psychopy.tests.test_visual.test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.visual`
- `psychopy.visual`
- `psychopy.tools.fontmanager`
- `pytest`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: Assign self.textbox.color = 'black'

```python
self.textbox.color = 'black'
```

### Step 2: Assign self.textbox.fillColor = 'white'

```python
self.textbox.fillColor = 'white'
```

### Step 3: Assign self.textbox.units = 'pix'

```python
self.textbox.units = 'pix'
```

### Step 4: Assign self.textbox.size = value

```python
self.textbox.size = (100, 50)
```

### Step 5: Assign self.textbox.pos = value

```python
self.textbox.pos = (0, 0)
```

### Step 6: Assign self.textbox.letterHeight = 5

```python
self.textbox.letterHeight = 5
```

### Step 7: Assign orientations = value

```python
orientations = [0, 120, 180, 240]
```

### Step 8: Assign anchors = value

```python
anchors = ['top left', 'center', 'bottom right']
```

### Step 9: Call self.win.flip()

```python
self.win.flip()
```

### Step 10: Assign self.textbox.ori = ori

```python
self.textbox.ori = ori
```

### Step 11: Assign self.textbox.anchor = anchor

```python
self.textbox.anchor = anchor
```

### Step 12: Call self.textbox._layout()

```python
self.textbox._layout()
```

### Step 13: Call self.textbox.draw()

```python
self.textbox.draw()
```

### Step 14: Assign exemplar = value

```python
exemplar = f'test_ori_{ori}_{anchor}.png'
```

### Step 15: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / 'Test_textbox' / exemplar, self.win, crit=20)
```


## Complete Example

```python
# Workflow
self.textbox.color = 'black'
self.textbox.fillColor = 'white'
self.textbox.units = 'pix'
self.textbox.size = (100, 50)
self.textbox.pos = (0, 0)
self.textbox.letterHeight = 5
orientations = [0, 120, 180, 240]
anchors = ['top left', 'center', 'bottom right']
for ori in orientations:
    for anchor in anchors:
        self.win.flip()
        self.textbox.ori = ori
        self.textbox.anchor = anchor
        self.textbox._layout()
        self.textbox.draw()
        exemplar = f'test_ori_{ori}_{anchor}.png'
        utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / 'Test_textbox' / exemplar, self.win, crit=20)
```

## Next Steps


---

*Source: test_textbox.py:107 | Complexity: Advanced | Last updated: 2026-05-18*