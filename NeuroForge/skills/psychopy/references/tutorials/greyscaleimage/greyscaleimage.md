# How To: Greyscaleimage

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test greyscaleImage

## Prerequisites

**Required Modules:**
- `sys`
- `os`
- `copy`
- `pathlib`
- `psychopy`
- `psychopy.visual`
- `psychopy.tools.coordinatetools`
- `psychopy.tests`
- `numpy`
- `pytest`
- `shutil`
- `tempfile`
- `psychopy.tests`
- `psychopy.tools`
- `psychopy.visual`


## Step-by-Step Guide

### Step 1: Assign win = value

```python
win = self.win
```

### Step 2: Assign fileName = os.path.join(...)

```python
fileName = os.path.join(utils.TESTS_DATA_PATH, 'greyscale.jpg')
```

### Step 3: Assign imageStim = visual.ImageStim(...)

```python
imageStim = visual.ImageStim(win, fileName)
```

### Step 4: Call imageStim.draw()

```python
imageStim.draw()
```

### Step 5: Call utils.compareScreenshot()

```python
utils.compareScreenshot('greyscale_%s.png' % self.contextName, win)
```

### Step 6: Call unknown.format()

```python
'{}'.format(imageStim)
```

### Step 7: Call win.flip()

```python
win.flip()
```

### Step 8: Assign imageStim.color = value

```python
imageStim.color = [0.1, 0.1, 0.1]
```

### Step 9: Call imageStim.draw()

```python
imageStim.draw()
```

### Step 10: Call utils.compareScreenshot()

```python
utils.compareScreenshot('greyscaleLowContr_%s.png' % self.contextName, win)
```

### Step 11: Call win.flip()

```python
win.flip()
```

### Step 12: Assign imageStim.color = 1

```python
imageStim.color = 1
```

### Step 13: Assign imageStim.contrast = 0.1

```python
imageStim.contrast = 0.1
```

### Step 14: Call imageStim.draw()

```python
imageStim.draw()
```

### Step 15: Call utils.compareScreenshot()

```python
utils.compareScreenshot('greyscaleLowContr_%s.png' % self.contextName, win)
```

### Step 16: Call win.flip()

```python
win.flip()
```

### Step 17: Assign imageStim.contrast = 1.0

```python
imageStim.contrast = 1.0
```

### Step 18: Assign fileName = os.path.join(...)

```python
fileName = os.path.join(utils.TESTS_DATA_PATH, 'greyscale2.png')
```

### Step 19: Assign imageStim.image = fileName

```python
imageStim.image = fileName
```

### Step 20: Call imageStim.draw()

```python
imageStim.draw()
```

### Step 21: Call utils.compareScreenshot()

```python
utils.compareScreenshot('greyscale2_%s.png' % self.contextName, win)
```

### Step 22: Call win.flip()

```python
win.flip()
```


## Complete Example

```python
# Workflow
win = self.win
fileName = os.path.join(utils.TESTS_DATA_PATH, 'greyscale.jpg')
imageStim = visual.ImageStim(win, fileName)
imageStim.draw()
utils.compareScreenshot('greyscale_%s.png' % self.contextName, win)
'{}'.format(imageStim)
win.flip()
imageStim.color = [0.1, 0.1, 0.1]
imageStim.draw()
utils.compareScreenshot('greyscaleLowContr_%s.png' % self.contextName, win)
win.flip()
imageStim.color = 1
imageStim.contrast = 0.1
imageStim.draw()
utils.compareScreenshot('greyscaleLowContr_%s.png' % self.contextName, win)
win.flip()
imageStim.contrast = 1.0
fileName = os.path.join(utils.TESTS_DATA_PATH, 'greyscale2.png')
imageStim.image = fileName
imageStim.size *= 3
imageStim.draw()
utils.compareScreenshot('greyscale2_%s.png' % self.contextName, win)
win.flip()
```

## Next Steps


---

*Source: test_all_stimuli.py:143 | Complexity: Advanced | Last updated: 2026-05-18*