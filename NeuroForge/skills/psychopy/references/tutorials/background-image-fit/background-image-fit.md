# How To: Background Image Fit

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test background image fit

## Prerequisites

**Required Modules:**
- `importlib`
- `copy`
- `pathlib`
- `psychopy`
- `psychopy.tests`
- `psychopy.tests.test_visual.test_basevisual`
- `psychopy.tools.stimulustools`
- `psychopy`


## Step-by-Step Guide

### Step 1: Assign _baseCases = value

```python
_baseCases = [{'fit': None, 'image': 'default.png', 'sizes': {'wide': 256, 'tall': 256, 'large': 256, 'small': 256}}, {'fit': 'cover', 'image': 'default.png', 'sizes': {'wide': 500, 'tall': 500, 'large': 500, 'small': 200}}, {'fit': 'contain', 'image': 'default.png', 'sizes': {'wide': 200, 'tall': 200, 'large': 500, 'small': 200}}, {'fit': 'fill', 'image': 'default.png', 'sizes': {'wide': 'fill', 'tall': 'fill', 'large': 500, 'small': 200}}, {'fit': 'scaleDown', 'image': 'default.png', 'sizes': {'wide': 200, 'tall': 200, 'large': 256, 'small': 200}}]
```

### Step 2: Assign cases = value

```python
cases = []
```

### Step 3: Assign sizes = value

```python
sizes = {'wide': (500, 200), 'tall': (200, 500), 'large': (500, 500), 'small': (200, 200)}
```

### Step 4: Assign theseCases = copy(...)

```python
theseCases = copy(_baseCases)
```

### Step 5: Assign win = visual.Window(...)

```python
win = visual.Window(size=size)
```

### Step 6: Call win.close()

```python
win.close()
```

### Step 7: Assign unknown = units

```python
case['units'] = units
```

### Step 8: Call cases.append()

```python
cases.append(case)
```

### Step 9: Assign win.backgroundFit = value

```python
win.backgroundFit = case['fit']
```

### Step 10: Assign win.backgroundImage = value

```python
win.backgroundImage = case['image']
```

### Step 11: Call win.flip()

```python
win.flip()
```

### Step 12: Assign imgName = value

```python
imgName = Path(case['image']).stem
```

### Step 13: Assign filename = value

```python
filename = f"test_win_bg_{sizeTag}_{case['sizes'][sizeTag]}_{imgName}.png"
```

### Step 14: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, win, crit=7)
```


## Complete Example

```python
# Workflow
_baseCases = [{'fit': None, 'image': 'default.png', 'sizes': {'wide': 256, 'tall': 256, 'large': 256, 'small': 256}}, {'fit': 'cover', 'image': 'default.png', 'sizes': {'wide': 500, 'tall': 500, 'large': 500, 'small': 200}}, {'fit': 'contain', 'image': 'default.png', 'sizes': {'wide': 200, 'tall': 200, 'large': 500, 'small': 200}}, {'fit': 'fill', 'image': 'default.png', 'sizes': {'wide': 'fill', 'tall': 'fill', 'large': 500, 'small': 200}}, {'fit': 'scaleDown', 'image': 'default.png', 'sizes': {'wide': 200, 'tall': 200, 'large': 256, 'small': 200}}]
cases = []
for units in ['pix', 'height', 'norm']:
    theseCases = copy(_baseCases)
    for case in theseCases:
        case['units'] = units
        cases.append(case)
sizes = {'wide': (500, 200), 'tall': (200, 500), 'large': (500, 500), 'small': (200, 200)}
for sizeTag, size in sizes.items():
    win = visual.Window(size=size)
    for case in cases:
        win.backgroundFit = case['fit']
        win.backgroundImage = case['image']
        win.flip()
        imgName = Path(case['image']).stem
        filename = f"test_win_bg_{sizeTag}_{case['sizes'][sizeTag]}_{imgName}.png"
        try:
            utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, win, crit=7)
        except AssertionError as err:
            raise AssertionError(f"Window did not look as expected when:\nbackgroundImage={case['image']},\nbackgroundFit={case['fit']},\nsize={sizeTag},\nunits={case['units']}\n\nOriginal error:{err}")
    win.close()
```

## Next Steps


---

*Source: test_window.py:27 | Complexity: Advanced | Last updated: 2026-05-18*