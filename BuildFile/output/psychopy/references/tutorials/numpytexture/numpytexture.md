# How To: Numpytexture

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test numpyTexture

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

### Step 2: Assign grating = filters.makeGrating(...)

```python
grating = filters.makeGrating(res=64, ori=20.0, cycles=3.0, phase=0.5, gratType='sqr', contr=1.0)
```

### Step 3: Assign imageStim = visual.ImageStim(...)

```python
imageStim = visual.ImageStim(win, image=grating, size=3 * self.scaleFactor, interpolate=True)
```

### Step 4: Call imageStim.draw()

```python
imageStim.draw()
```

### Step 5: Call utils.compareScreenshot()

```python
utils.compareScreenshot('numpyImage_%s.png' % self.contextName, win)
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
utils.compareScreenshot('numpyLowContr_%s.png' % self.contextName, win)
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
utils.compareScreenshot('numpyLowContr_%s.png' % self.contextName, win)
```

### Step 16: Call win.flip()

```python
win.flip()
```


## Complete Example

```python
# Workflow
win = self.win
grating = filters.makeGrating(res=64, ori=20.0, cycles=3.0, phase=0.5, gratType='sqr', contr=1.0)
imageStim = visual.ImageStim(win, image=grating, size=3 * self.scaleFactor, interpolate=True)
imageStim.draw()
utils.compareScreenshot('numpyImage_%s.png' % self.contextName, win)
'{}'.format(imageStim)
win.flip()
imageStim.color = [0.1, 0.1, 0.1]
imageStim.draw()
utils.compareScreenshot('numpyLowContr_%s.png' % self.contextName, win)
win.flip()
imageStim.color = 1
imageStim.contrast = 0.1
imageStim.draw()
utils.compareScreenshot('numpyLowContr_%s.png' % self.contextName, win)
win.flip()
```

## Next Steps


---

*Source: test_all_stimuli.py:168 | Complexity: Advanced | Last updated: 2026-05-18*