# How To: Text With Add

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test text with add

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

### Step 2: Assign text = visual.TextStim(...)

```python
text = visual.TextStim(win, pos=[0, 0.9])
```

### Step 3: Assign grat1 = visual.GratingStim(...)

```python
grat1 = visual.GratingStim(win, size=2 * self.scaleFactor, opacity=0.5, pos=[0.3, 0.0], ori=45, sf=2 * self.scaleFactor)
```

### Step 4: Assign grat2 = visual.GratingStim(...)

```python
grat2 = visual.GratingStim(win, size=2 * self.scaleFactor, opacity=0.5, pos=[-0.3, 0.0], ori=-45, sf=2 * self.scaleFactor)
```

### Step 5: Call text.draw()

```python
text.draw()
```

### Step 6: Call grat1.draw()

```python
grat1.draw()
```

### Step 7: Call grat2.draw()

```python
grat2.draw()
```

### Step 8: Call pytest.skip()

```python
pytest.skip("Blendmode='add' doesn't work under a virtual machine for some reason")
```

### Step 9: Call utils.compareScreenshot()

```python
utils.compareScreenshot('blend_add_%s.png' % self.contextName, win, crit=20)
```


## Complete Example

```python
# Workflow
win = self.win
text = visual.TextStim(win, pos=[0, 0.9])
grat1 = visual.GratingStim(win, size=2 * self.scaleFactor, opacity=0.5, pos=[0.3, 0.0], ori=45, sf=2 * self.scaleFactor)
grat2 = visual.GratingStim(win, size=2 * self.scaleFactor, opacity=0.5, pos=[-0.3, 0.0], ori=-45, sf=2 * self.scaleFactor)
text.draw()
grat1.draw()
grat2.draw()
if systemtools.isVM_CI():
    pytest.skip("Blendmode='add' doesn't work under a virtual machine for some reason")
if self.win.winType != 'pygame':
    utils.compareScreenshot('blend_add_%s.png' % self.contextName, win, crit=20)
```

## Next Steps


---

*Source: test_all_stimuli.py:259 | Complexity: Advanced | Last updated: 2026-05-18*