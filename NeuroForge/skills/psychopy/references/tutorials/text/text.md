# How To: Text

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test text

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

### Step 2: Assign fontFile = str(...)

```python
fontFile = str(utils.TESTS_FONT)
```

### Step 3: Assign stim = visual.TextStim(...)

```python
stim = visual.TextStim(win, text=u'Ψa', color=[0.5, 1.0, 1.0], ori=15, height=0.8 * self.scaleFactor, pos=[0, 0], font='DejaVu Serif', fontFiles=[fontFile])
```

### Step 4: Call stim.draw()

```python
stim.draw()
```

### Step 5: Call win.flip()

```python
win.flip()
```

### Step 6: Assign stim.text = 'y'

```python
stim.text = 'y'
```

### Step 7: Assign stim.ori = value

```python
stim.ori = -30.5
```

### Step 8: Assign stim.height = value

```python
stim.height = 1.0 * self.scaleFactor
```

### Step 9: Call stim.setColor()

```python
stim.setColor([0.1, -1, 0.8], colorSpace='rgb')
```

### Step 10: Assign stim.contrast = 0.8

```python
stim.contrast = 0.8
```

### Step 11: Assign stim.opacity = 0.8

```python
stim.opacity = 0.8
```

### Step 12: Call stim.draw()

```python
stim.draw()
```

### Step 13: Call unknown.format()

```python
'{}'.format(stim)
```

### Step 14: Call utils.compareScreenshot()

```python
utils.compareScreenshot('text1_%s.png' % self.contextName, win, crit=20)
```

### Step 15: Assign stim.font = 'Courier New'

```python
stim.font = 'Courier New'
```

### Step 16: Assign stim.font = 'Courier'

```python
stim.font = 'Courier'
```

### Step 17: Call utils.compareScreenshot()

```python
utils.compareScreenshot('text2_%s.png' % self.contextName, win, crit=20)
```


## Complete Example

```python
# Workflow
win = self.win
fontFile = str(utils.TESTS_FONT)
stim = visual.TextStim(win, text=u'Ψa', color=[0.5, 1.0, 1.0], ori=15, height=0.8 * self.scaleFactor, pos=[0, 0], font='DejaVu Serif', fontFiles=[fontFile])
stim.draw()
if self.win.winType != 'pygame':
    utils.compareScreenshot('text1_%s.png' % self.contextName, win, crit=20)
win.flip()
stim.text = 'y'
if sys.platform == 'win32':
    stim.font = 'Courier New'
else:
    stim.font = 'Courier'
stim.ori = -30.5
stim.height = 1.0 * self.scaleFactor
stim.setColor([0.1, -1, 0.8], colorSpace='rgb')
stim.pos += [-0.5, 0.5]
stim.contrast = 0.8
stim.opacity = 0.8
stim.draw()
'{}'.format(stim)
if self.win.winType != 'pygame':
    utils.compareScreenshot('text2_%s.png' % self.contextName, win, crit=20)
```

## Next Steps


---

*Source: test_all_stimuli.py:227 | Complexity: Advanced | Last updated: 2026-05-18*