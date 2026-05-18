# How To: Win Color With Image

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that the window color is still visible under the background image

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

### Step 1: '\n        Test that the window color is still visible under the background image\n        '

```python
'\n        Test that the window color is still visible under the background image\n        '
```

### Step 2: Assign cases = value

```python
cases = ['red', 'blue', 'green']
```

### Step 3: Assign win = visual.Window(...)

```python
win = visual.Window(size=(200, 200), backgroundImage='default.png', backgroundFit='contain')
```

### Step 4: Assign win.color = case

```python
win.color = case
```

### Step 5: Call win.flip()

```python
win.flip()
```

### Step 6: Assign filename = value

```python
filename = f'test_win_bgcolor_{case}.png'
```

### Step 7: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, win, crit=10)
```


## Complete Example

```python
# Workflow
'\n        Test that the window color is still visible under the background image\n        '
cases = ['red', 'blue', 'green']
win = visual.Window(size=(200, 200), backgroundImage='default.png', backgroundFit='contain')
for case in cases:
    win.color = case
    win.flip()
    filename = f'test_win_bgcolor_{case}.png'
    utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, win, crit=10)
```

## Next Steps


---

*Source: test_window.py:86 | Complexity: Intermediate | Last updated: 2026-05-18*