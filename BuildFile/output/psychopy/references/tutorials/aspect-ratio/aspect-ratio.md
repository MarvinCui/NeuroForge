# How To: Aspect Ratio

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that images set with one or both dimensions as None maintain their aspect ratio

## Prerequisites

**Required Modules:**
- `pathlib`
- `psychopy`
- `test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.tests`
- `pytest`


## Step-by-Step Guide

### Step 1: '\n        Test that images set with one or both dimensions as None maintain their aspect ratio\n        '

```python
'\n        Test that images set with one or both dimensions as None maintain their aspect ratio\n        '
```

**Verification:**
```python
assert self.obj.aspectRatio == case['aspect']
```

### Step 2: Assign cases = value

```python
cases = [{'img': 'default.png', 'aspect': (1, 1), 'size': (None, 2), 'units': 'norm', 'tag': 'default_xNone_yFull'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (2, None), 'units': 'norm', 'tag': 'default_xFull_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, None), 'units': 'norm', 'tag': 'default_xNone_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': None, 'units': 'norm', 'tag': 'default_None'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, 1), 'units': 'height', 'tag': 'default_xNone_yFull'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (1 / self.win.size[1] * self.win.size[0], None), 'units': 'height', 'tag': 'default_xFull_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, None), 'units': 'height', 'tag': 'default_xNone_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': None, 'units': 'height', 'tag': 'default_None'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, self.win.size[1]), 'units': 'pix', 'tag': 'default_xNone_yFull'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (self.win.size[0], None), 'units': 'pix', 'tag': 'default_xFull_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, None), 'units': 'pix', 'tag': 'default_xNone_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': None, 'units': 'pix', 'tag': 'default_None'}]
```

### Step 3: Assign self.obj.image = value

```python
self.obj.image = case['img']
```

### Step 4: Assign self.obj.units = value

```python
self.obj.units = case['units']
```

### Step 5: Assign self.obj.size = value

```python
self.obj.size = case['size']
```

**Verification:**
```python
assert self.obj.aspectRatio == case['aspect']
```

### Step 6: Call self.obj.draw()

```python
self.obj.draw()
```

### Step 7: Assign filename = value

```python
filename = f"test_image_aspect_{case['tag']}.png"
```

### Step 8: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=7)
```

### Step 9: Call self.win.flip()

```python
self.win.flip()
```


## Complete Example

```python
# Workflow
'\n        Test that images set with one or both dimensions as None maintain their aspect ratio\n        '
cases = [{'img': 'default.png', 'aspect': (1, 1), 'size': (None, 2), 'units': 'norm', 'tag': 'default_xNone_yFull'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (2, None), 'units': 'norm', 'tag': 'default_xFull_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, None), 'units': 'norm', 'tag': 'default_xNone_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': None, 'units': 'norm', 'tag': 'default_None'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, 1), 'units': 'height', 'tag': 'default_xNone_yFull'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (1 / self.win.size[1] * self.win.size[0], None), 'units': 'height', 'tag': 'default_xFull_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, None), 'units': 'height', 'tag': 'default_xNone_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': None, 'units': 'height', 'tag': 'default_None'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, self.win.size[1]), 'units': 'pix', 'tag': 'default_xNone_yFull'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (self.win.size[0], None), 'units': 'pix', 'tag': 'default_xFull_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, None), 'units': 'pix', 'tag': 'default_xNone_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': None, 'units': 'pix', 'tag': 'default_None'}]
for case in cases:
    self.obj.image = case['img']
    self.obj.units = case['units']
    self.obj.size = case['size']
    assert self.obj.aspectRatio == case['aspect']
    self.obj.draw()
    filename = f"test_image_aspect_{case['tag']}.png"
    utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=7)
    self.win.flip()
```

## Next Steps


---

*Source: test_image.py:48 | Complexity: Advanced | Last updated: 2026-05-18*