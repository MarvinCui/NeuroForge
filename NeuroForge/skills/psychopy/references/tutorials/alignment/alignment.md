# How To: Alignment

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test alignment

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

### Step 1: Assign exemplars = value

```python
exemplars = ['top left', 'top center', 'top right', 'center left', 'center center', 'center right', 'bottom left', 'bottom center', 'bottom right']
```

### Step 2: Assign tykes = value

```python
tykes = ['center', 'centre', 'centre centre', 'someword', 'more than two words']
```

### Step 3: Assign initParams = value

```python
initParams = {}
```

### Step 4: Assign unknown = getattr(...)

```python
initParams[param] = getattr(self.textbox, param)
```

### Step 5: Call setattr()

```python
setattr(self.textbox, param, value)
```

### Step 6: Assign self.textbox.text = 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question.'

```python
self.textbox.text = 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question.'
```

### Step 7: Assign self.textbox.fillColor = 'white'

```python
self.textbox.fillColor = 'white'
```

### Step 8: Assign self.textbox.color = 'black'

```python
self.textbox.color = 'black'
```

### Step 9: Assign self.textbox.padding = 0

```python
self.textbox.padding = 0
```

### Step 10: Assign self.textbox.letterHeight = layout.Size(...)

```python
self.textbox.letterHeight = layout.Size((0, 10), units='pix', win=self.win)
```

### Step 11: Assign self.textbox.units = units

```python
self.textbox.units = units
```

### Step 12: Assign self.textbox.alignment = case

```python
self.textbox.alignment = case
```

### Step 13: Call self.textbox.draw()

```python
self.textbox.draw()
```

### Step 14: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / f"textbox_{self.textbox._lineBreaking}_align_{case.replace(' ', '_')}.png", self.win, crit=20)
```

### Step 15: Call self.win.flip()

```python
self.win.flip()
```


## Complete Example

```python
# Workflow
exemplars = ['top left', 'top center', 'top right', 'center left', 'center center', 'center right', 'bottom left', 'bottom center', 'bottom right']
tykes = ['center', 'centre', 'centre centre', 'someword', 'more than two words']
initParams = {}
for param in ['units', 'fillColor', 'color', 'padding', 'letterHeight', 'alignment', 'text']:
    initParams[param] = getattr(self.textbox, param)
for case in exemplars + tykes:
    for units in layout.unitTypes:
        self.textbox.text = 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question.'
        self.textbox.fillColor = 'white'
        self.textbox.color = 'black'
        self.textbox.padding = 0
        self.textbox.letterHeight = layout.Size((0, 10), units='pix', win=self.win)
        self.textbox.units = units
        self.textbox.alignment = case
        self.textbox.draw()
        utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / f"textbox_{self.textbox._lineBreaking}_align_{case.replace(' ', '_')}.png", self.win, crit=20)
        self.win.flip()
for param, value in initParams.items():
    setattr(self.textbox, param, value)
```

## Next Steps


---

*Source: test_textbox.py:503 | Complexity: Advanced | Last updated: 2026-05-18*