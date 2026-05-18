# How To: Capturemovieframes

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test captureMovieFrames

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

### Step 1: Assign stim = visual.GratingStim(...)

```python
stim = visual.GratingStim(self.win, dkl=[0, 0, 1])
```

### Step 2: Assign stim.autoDraw = True

```python
stim.autoDraw = True
```

### Step 3: Call self.win.saveMovieFrames()

```python
self.win.saveMovieFrames(os.path.join(self.temp_dir, 'junkFrames.png'))
```

### Step 4: Call self.win.saveMovieFrames()

```python
self.win.saveMovieFrames(os.path.join(self.temp_dir, 'junkFrames.gif'))
```

### Step 5: Assign region = self.win._getRegionOfFrame(...)

```python
region = self.win._getRegionOfFrame()
```

### Step 6: Call self.win.flip()

```python
self.win.flip()
```

### Step 7: Call self.win.getMovieFrame()

```python
self.win.getMovieFrame()
```


## Complete Example

```python
# Workflow
stim = visual.GratingStim(self.win, dkl=[0, 0, 1])
stim.autoDraw = True
for frameN in range(3):
    stim.phase += 0.3
    self.win.flip()
    self.win.getMovieFrame()
self.win.saveMovieFrames(os.path.join(self.temp_dir, 'junkFrames.png'))
self.win.saveMovieFrames(os.path.join(self.temp_dir, 'junkFrames.gif'))
region = self.win._getRegionOfFrame()
```

## Next Steps


---

*Source: test_all_stimuli.py:34 | Complexity: Intermediate | Last updated: 2026-05-18*