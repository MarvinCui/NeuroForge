# How To: Unit Mismatch

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that a given stimulus can be drawn without error in all combinations of stimulus units x window units and
checking that it looks the same as when both units are pix.

## Prerequisites

**Required Modules:**
- `json`
- `pytest`
- `importlib`
- `copy`
- `pathlib`
- `psychopy`
- `psychopy.tools.stimulustools`
- `psychopy.monitors`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: '\n        Test that a given stimulus can be drawn without error in all combinations of stimulus units x window units and\n        checking that it looks the same as when both units are pix.\n        '

```python
'\n        Test that a given stimulus can be drawn without error in all combinations of stimulus units x window units and\n        checking that it looks the same as when both units are pix.\n        '
```

**Verification:**
```python
assert layout.Size(obj.size, obj.units, obj.win) == layout.Size(targetSizes[objunits], objunits, obj.win), f'Object size ({obj.size}, in {obj.units}) did not match desired size ({targetSizes[objunits]} in {objunits} when window was {obj.win.size}px in {winunits}.'
```

### Step 2: Assign unitTypes = value

```python
unitTypes = layout.unitTypes[2:]
```

### Step 3: Assign win = visual.Window(...)

```python
win = visual.Window(self.obj.win.size, pos=self.obj.win.pos, monitor='testMonitor')
```

### Step 4: Assign obj = copy(...)

```python
obj = copy(self.obj)
```

### Step 5: Assign obj.win = win

```python
obj.win = win
```

### Step 6: Assign win.units = 'pix'

```python
win.units = 'pix'
```

### Step 7: Assign obj.units = 'pix'

```python
obj.units = 'pix'
```

### Step 8: Call obj.draw()

```python
obj.draw()
```

### Step 9: Assign filename = value

```python
filename = Path(utils.TESTS_DATA_PATH) / 'test_unit_mismatch.png'
```

### Step 10: Call win.getMovieFrame.save()

```python
win.getMovieFrame(buffer='back').save(filename)
```

### Step 11: Call win.flip()

```python
win.flip()
```

### Step 12: Call win.close()

```python
win.close()
```

### Step 13: Call filename.unlink()

```python
filename.unlink()
```

### Step 14: Assign targetSizes = value

```python
targetSizes = {units: getattr(obj._size, units) for units in unitTypes}
```

### Step 15: Assign win.units = winunits

```python
win.units = winunits
```

### Step 16: Assign obj.units = objunits

```python
obj.units = objunits
```

### Step 17: Call obj.draw()

```python
obj.draw()
```

### Step 18: Call utils.compareScreenshot()

```python
utils.compareScreenshot(filename, win, tag=f'{winunits}X{objunits}')
```

### Step 19: Call win.flip()

```python
win.flip()
```

**Verification:**
```python
assert layout.Size(obj.size, obj.units, obj.win) == layout.Size(targetSizes[objunits], objunits, obj.win), f'Object size ({obj.size}, in {obj.units}) did not match desired size ({targetSizes[objunits]} in {objunits} when window was {obj.win.size}px in {winunits}.'
```


## Complete Example

```python
# Workflow
'\n        Test that a given stimulus can be drawn without error in all combinations of stimulus units x window units and\n        checking that it looks the same as when both units are pix.\n        '
unitTypes = layout.unitTypes[2:]
win = visual.Window(self.obj.win.size, pos=self.obj.win.pos, monitor='testMonitor')
obj = copy(self.obj)
obj.win = win
win.units = 'pix'
obj.units = 'pix'
obj.draw()
filename = Path(utils.TESTS_DATA_PATH) / 'test_unit_mismatch.png'
win.getMovieFrame(buffer='back').save(filename)
if hasattr(obj, '_size'):
    targetSizes = {units: getattr(obj._size, units) for units in unitTypes}
win.flip()
for winunits in unitTypes:
    for objunits in unitTypes:
        win.units = winunits
        obj.units = objunits
        obj.draw()
        utils.compareScreenshot(filename, win, tag=f'{winunits}X{objunits}')
        if hasattr(obj, '_size'):
            assert layout.Size(obj.size, obj.units, obj.win) == layout.Size(targetSizes[objunits], objunits, obj.win), f'Object size ({obj.size}, in {obj.units}) did not match desired size ({targetSizes[objunits]} in {objunits} when window was {obj.win.size}px in {winunits}.'
        win.flip()
win.close()
filename.unlink()
```

## Next Steps


---

*Source: test_basevisual.py:419 | Complexity: Advanced | Last updated: 2026-05-18*