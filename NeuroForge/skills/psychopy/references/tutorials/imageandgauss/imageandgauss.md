# How To: Imageandgauss

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test imageAndGauss

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
fileName = os.path.join(utils.TESTS_DATA_PATH, 'testimage.jpg')
```

### Step 3: Assign size = value

```python
size = numpy.array([2.0, 2.0]) * self.scaleFactor
```

### Step 4: Assign image = visual.ImageStim(...)

```python
image = visual.ImageStim(win, image=fileName, mask='gauss', size=size, flipHoriz=True, flipVert=True)
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


## Complete Example

```python
# Workflow
win = self.win
fileName = os.path.join(utils.TESTS_DATA_PATH, 'testimage.jpg')
size = numpy.array([2.0, 2.0]) * self.scaleFactor
image = visual.ImageStim(win, image=fileName, mask='gauss', size=size, flipHoriz=True, flipVert=True)
image.draw()
utils.compareScreenshot('imageAndGauss_%s.png' % self.contextName, win)
win.flip()
```

## Next Steps


---

*Source: test_all_stimuli.py:103 | Complexity: Intermediate | Last updated: 2026-05-18*