# How To: Speechpoint

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test speechpoint

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

### Step 1: Assign self.obj.size = value

```python
self.obj.size = (0.5, 0.5)
```

### Step 2: Assign self.obj.fillColor = 'red'

```python
self.obj.fillColor = 'red'
```

### Step 3: Assign cases = value

```python
cases = [(-3 / 8, 0), (3 / 8, 0), (0, -3 / 8), (0, 3 / 8)]
```

### Step 4: Assign self.obj.speechPoint = None

```python
self.obj.speechPoint = None
```

### Step 5: Call self.win.flip()

```python
self.win.flip()
```

### Step 6: Assign self.obj.speechPoint = value

```python
self.obj.speechPoint = (x, y)
```

### Step 7: Call self.obj.draw()

```python
self.obj.draw()
```

### Step 8: Assign filename = value

```python
filename = f'{self.__class__.__name__}_testSpeechpoint_{int(x * 8)}ovr8_{int(y * 8)}ovr8.png'
```

### Step 9: Call utils.compareScreenshot()

```python
utils.compareScreenshot(filename, self.win, crit=8)
```


## Complete Example

```python
# Workflow
self.obj.size = (0.5, 0.5)
self.obj.fillColor = 'red'
cases = [(-3 / 8, 0), (3 / 8, 0), (0, -3 / 8), (0, 3 / 8)]
for x, y in cases:
    self.win.flip()
    self.obj.speechPoint = (x, y)
    self.obj.draw()
    filename = f'{self.__class__.__name__}_testSpeechpoint_{int(x * 8)}ovr8_{int(y * 8)}ovr8.png'
    utils.compareScreenshot(filename, self.win, crit=8)
self.obj.speechPoint = None
```

## Next Steps


---

*Source: test_textbox.py:549 | Complexity: Advanced | Last updated: 2026-05-18*