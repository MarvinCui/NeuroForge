# How To: Anchor Flip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that flipping the image doesn't flip the direction of the anchor

## Prerequisites

**Required Modules:**
- `pathlib`
- `psychopy`
- `test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.tests`
- `pytest`


## Step-by-Step Guide

### Step 1: "\n        Check that flipping the image doesn't flip the direction of the anchor\n        "

```python
"\n        Check that flipping the image doesn't flip the direction of the anchor\n        "
```

### Step 2: Assign self.obj.units = 'height'

```python
self.obj.units = 'height'
```

### Step 3: Assign self.obj.pos = value

```python
self.obj.pos = (0, 0)
```

### Step 4: Assign self.obj.size = value

```python
self.obj.size = (0.5, 0.5)
```

### Step 5: Assign self.obj.anchor = 'bottom left'

```python
self.obj.anchor = 'bottom left'
```

### Step 6: Assign self.obj.flipVert = True

```python
self.obj.flipVert = True
```

### Step 7: Assign self.obj.flipHoriz = False

```python
self.obj.flipHoriz = False
```

### Step 8: Call self.win.flip()

```python
self.win.flip()
```

### Step 9: Call self.obj.draw()

```python
self.obj.draw()
```

### Step 10: Call utils.compareScreenshot()

```python
utils.compareScreenshot('test_image_flip_anchor_vert.png', self.win, crit=7)
```

### Step 11: Assign self.obj.flipVert = False

```python
self.obj.flipVert = False
```

### Step 12: Assign self.obj.flipHoriz = True

```python
self.obj.flipHoriz = True
```

### Step 13: Call self.win.flip()

```python
self.win.flip()
```

### Step 14: Call self.obj.draw()

```python
self.obj.draw()
```

### Step 15: Call utils.compareScreenshot()

```python
utils.compareScreenshot('test_image_flip_anchor_horiz.png', self.win, crit=7)
```


## Complete Example

```python
# Workflow
"\n        Check that flipping the image doesn't flip the direction of the anchor\n        "
self.obj.units = 'height'
self.obj.pos = (0, 0)
self.obj.size = (0.5, 0.5)
self.obj.anchor = 'bottom left'
self.obj.flipVert = True
self.obj.flipHoriz = False
self.win.flip()
self.obj.draw()
utils.compareScreenshot('test_image_flip_anchor_vert.png', self.win, crit=7)
self.obj.flipVert = False
self.obj.flipHoriz = True
self.win.flip()
self.obj.draw()
utils.compareScreenshot('test_image_flip_anchor_horiz.png', self.win, crit=7)
```

## Next Steps


---

*Source: test_image.py:22 | Complexity: Advanced | Last updated: 2026-05-18*