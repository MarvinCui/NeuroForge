# How To: Gratingimageandgauss

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gratingImageAndGauss

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

### Step 2: Assign size = value

```python
size = numpy.array([2.0, 2.0]) * self.scaleFactor
```

### Step 3: Assign fileName = os.path.join(...)

```python
fileName = os.path.join(utils.TESTS_DATA_PATH, 'testimage.jpg')
```

### Step 4: Assign image = visual.GratingStim(...)

```python
image = visual.GratingStim(win, tex=fileName, size=size, sf=sf, mask='gauss')
```

### Step 5: Call image.draw()

```python
image.draw()
```

### Step 6: Call utils.compareScreenshot()

```python
utils.compareScreenshot('imageAndGauss_%s.png' % self.contextName, win)
```

### Step 7: Call win.flip()

```python
win.flip()
```

### Step 8: Assign sf = value

```python
sf = -1.0
```

### Step 9: Assign sf = value

```python
sf = -1.0 / size
```


## Complete Example

```python
# Workflow
win = self.win
size = numpy.array([2.0, 2.0]) * self.scaleFactor
fileName = os.path.join(utils.TESTS_DATA_PATH, 'testimage.jpg')
if win.units in ['norm', 'height']:
    sf = -1.0
else:
    sf = -1.0 / size
image = visual.GratingStim(win, tex=fileName, size=size, sf=sf, mask='gauss')
image.draw()
utils.compareScreenshot('imageAndGauss_%s.png' % self.contextName, win)
win.flip()
```

## Next Steps


---

*Source: test_all_stimuli.py:114 | Complexity: Advanced | Last updated: 2026-05-18*