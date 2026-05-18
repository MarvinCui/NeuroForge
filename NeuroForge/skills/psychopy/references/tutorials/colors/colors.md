# How To: Colors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test colors

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

### Step 1: Call _TestColorMixin.test_colors()

```python
_TestColorMixin.test_colors(self)
```

### Step 2: Assign self.textbox.text = 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.'

```python
self.textbox.text = 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.'
```

### Step 3: Assign exemplars = value

```python
exemplars = [{'color': (1, 1, 1), 'fillColor': (-1, -1, -1), 'borderColor': (-1, -1, -1), 'space': 'rgb', 'screenshot': 'colors_WOB.png'}, {'color': 'white', 'fillColor': 'black', 'borderColor': 'black', 'space': 'rgb', 'screenshot': 'colors_WOB.png'}, {'color': '#ffffff', 'fillColor': '#000000', 'borderColor': '#000000', 'space': 'hex', 'screenshot': 'colors_WOB.png'}, {'color': 'red', 'fillColor': 'yellow', 'borderColor': 'blue', 'space': 'rgb', 'screenshot': 'colors_exemplar1.png'}, {'color': 'yellow', 'fillColor': 'blue', 'borderColor': 'red', 'space': 'rgb', 'screenshot': 'colors_exemplar2.png'}, {'color': 'blue', 'fillColor': 'red', 'borderColor': 'yellow', 'space': 'rgb', 'screenshot': 'colors_exemplar3.png'}]
```

### Step 4: Assign tykes = value

```python
tykes = [{'color': 'white', 'fillColor': None, 'borderColor': None, 'space': 'rgb', 'screenshot': 'colors_tyke1.png'}, {'color': None, 'fillColor': 'white', 'borderColor': None, 'space': 'rgb', 'screenshot': 'colors_tyke2.png'}, {'color': None, 'fillColor': None, 'borderColor': 'white', 'space': 'rgb', 'screenshot': 'colors_tyke3.png'}]
```

### Step 5: Assign self.textbox.colorSpace = value

```python
self.textbox.colorSpace = case['space']
```

### Step 6: Assign self.textbox.color = value

```python
self.textbox.color = case['color']
```

### Step 7: Assign self.textbox.fillColor = value

```python
self.textbox.fillColor = case['fillColor']
```

### Step 8: Assign self.textbox.borderColor = value

```python
self.textbox.borderColor = case['borderColor']
```

### Step 9: Call self.win.flip()

```python
self.win.flip()
```

### Step 10: Call self.textbox.draw()

```python
self.textbox.draw()
```

### Step 11: Assign filename = unknown.format(...)

```python
filename = 'textbox_{}_{}'.format(self.textbox._lineBreaking, case['screenshot'])
```

### Step 12: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
```


## Complete Example

```python
# Workflow
_TestColorMixin.test_colors(self)
self.textbox.text = 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.'
exemplars = [{'color': (1, 1, 1), 'fillColor': (-1, -1, -1), 'borderColor': (-1, -1, -1), 'space': 'rgb', 'screenshot': 'colors_WOB.png'}, {'color': 'white', 'fillColor': 'black', 'borderColor': 'black', 'space': 'rgb', 'screenshot': 'colors_WOB.png'}, {'color': '#ffffff', 'fillColor': '#000000', 'borderColor': '#000000', 'space': 'hex', 'screenshot': 'colors_WOB.png'}, {'color': 'red', 'fillColor': 'yellow', 'borderColor': 'blue', 'space': 'rgb', 'screenshot': 'colors_exemplar1.png'}, {'color': 'yellow', 'fillColor': 'blue', 'borderColor': 'red', 'space': 'rgb', 'screenshot': 'colors_exemplar2.png'}, {'color': 'blue', 'fillColor': 'red', 'borderColor': 'yellow', 'space': 'rgb', 'screenshot': 'colors_exemplar3.png'}]
tykes = [{'color': 'white', 'fillColor': None, 'borderColor': None, 'space': 'rgb', 'screenshot': 'colors_tyke1.png'}, {'color': None, 'fillColor': 'white', 'borderColor': None, 'space': 'rgb', 'screenshot': 'colors_tyke2.png'}, {'color': None, 'fillColor': None, 'borderColor': 'white', 'space': 'rgb', 'screenshot': 'colors_tyke3.png'}]
for case in exemplars + tykes:
    if not all((key in case for key in ['color', 'fillColor', 'borderColor', 'space', 'screenshot'])):
        raise KeyError(f'Case spec for test_colors in class {self.__class__.__name__} ({__file__}) invalid, test cannot be run.')
    self.textbox.colorSpace = case['space']
    self.textbox.color = case['color']
    self.textbox.fillColor = case['fillColor']
    self.textbox.borderColor = case['borderColor']
    for lineBreaking in ('default', 'uax14'):
        self.win.flip()
        self.textbox.draw()
    if case['screenshot']:
        filename = 'textbox_{}_{}'.format(self.textbox._lineBreaking, case['screenshot'])
        utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
```

## Next Steps


---

*Source: test_textbox.py:143 | Complexity: Advanced | Last updated: 2026-05-18*