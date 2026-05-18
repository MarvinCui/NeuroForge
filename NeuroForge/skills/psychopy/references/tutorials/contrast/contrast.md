# How To: Contrast

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test contrast

## Prerequisites

**Required Modules:**
- `psychopy.alerts`
- `psychopy.alerts._errorHandler`
- `psychopy.tests`
- `psychopy`
- `numpy`


## Step-by-Step Guide

### Step 1: Assign obj = visual.Rect(...)

```python
obj = visual.Rect(self.win, units='pix', pos=(0, 0), size=(128, 128), lineWidth=10)
```

### Step 2: Assign obj.fillColor = 'red'

```python
obj.fillColor = 'red'
```

### Step 3: Assign obj.borderColor = 'blue'

```python
obj.borderColor = 'blue'
```

### Step 4: Assign obj.opacity = 1

```python
obj.opacity = 1
```

### Step 5: Assign obj.contrast = 0.5

```python
obj.contrast = 0.5
```

### Step 6: Call self.win.flip()

```python
self.win.flip()
```

### Step 7: Call obj.draw()

```python
obj.draw()
```

### Step 8: Call utils.comparePixelColor()

```python
utils.comparePixelColor(self.win, colors.Color((0.5, -0.5, -0.5), 'rgb'), coord=(50, 50))
```

### Step 9: Call utils.comparePixelColor()

```python
utils.comparePixelColor(self.win, colors.Color((-0.5, -0.5, 0.5), 'rgb'), coord=(1, 1))
```


## Complete Example

```python
# Workflow
obj = visual.Rect(self.win, units='pix', pos=(0, 0), size=(128, 128), lineWidth=10)
obj.fillColor = 'red'
obj.borderColor = 'blue'
obj.opacity = 1
obj.contrast = 0.5
self.win.flip()
obj.draw()
utils.comparePixelColor(self.win, colors.Color((0.5, -0.5, -0.5), 'rgb'), coord=(50, 50))
utils.comparePixelColor(self.win, colors.Color((-0.5, -0.5, 0.5), 'rgb'), coord=(1, 1))
```

## Next Steps


---

*Source: test_color.py:182 | Complexity: Advanced | Last updated: 2026-05-18*