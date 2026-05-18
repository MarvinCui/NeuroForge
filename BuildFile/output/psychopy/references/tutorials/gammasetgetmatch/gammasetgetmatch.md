# How To: Gammasetgetmatch

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test that repeatedly getting and setting the gamma table has no
cumulative effect.

## Prerequisites

**Required Modules:**
- `psychopy`
- `numpy`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: 'test that repeatedly getting and setting the gamma table has no\n    cumulative effect.'

```python
'test that repeatedly getting and setting the gamma table has no\n    cumulative effect.'
```

**Verification:**
```python
assert numpy.all(currGammaTable == startGammaTable)
```

### Step 2: Assign startGammaTable = None

```python
startGammaTable = None
```

### Step 3: Assign n_repeats = 2

```python
n_repeats = 2
```

### Step 4: Assign win = visual.Window(...)

```python
win = visual.Window([600, 600], autoLog=False)
```

### Step 5: Call win.close()

```python
win.close()
```

### Step 6: Call win.flip()

```python
win.flip()
```

### Step 7: Assign startGammaTable = win.backend.getGammaRamp(...)

```python
startGammaTable = win.backend.getGammaRamp()
```

### Step 8: Assign currGammaTable = win.backend.getGammaRamp(...)

```python
currGammaTable = win.backend.getGammaRamp()
```

**Verification:**
```python
assert numpy.all(currGammaTable == startGammaTable)
```


## Complete Example

```python
# Workflow
'test that repeatedly getting and setting the gamma table has no\n    cumulative effect.'
startGammaTable = None
n_repeats = 2
for _ in range(n_repeats):
    win = visual.Window([600, 600], autoLog=False)
    for _ in range(5):
        win.flip()
    if startGammaTable is None:
        startGammaTable = win.backend.getGammaRamp()
    else:
        currGammaTable = win.backend.getGammaRamp()
        assert numpy.all(currGammaTable == startGammaTable)
    win.close()
```

## Next Steps


---

*Source: test_gamma.py:126 | Complexity: Advanced | Last updated: 2026-05-18*