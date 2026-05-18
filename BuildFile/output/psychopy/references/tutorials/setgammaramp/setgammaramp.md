# How To: Setgammaramp

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test that the gamma ramp is set as requested

## Prerequisites

**Required Modules:**
- `psychopy`
- `numpy`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: 'test that the gamma ramp is set as requested'

```python
'test that the gamma ramp is set as requested'
```

**Verification:**
```python
assert numpy.allclose(desiredRamp, setRamp, atol=1.0 / desiredRamp.shape[1])
```

### Step 2: Assign testGamma = 2.2

```python
testGamma = 2.2
```

### Step 3: Assign win = visual.Window(...)

```python
win = visual.Window([600, 600], autoLog=False)
```

### Step 4: Assign desiredRamp = numpy.tile(...)

```python
desiredRamp = numpy.tile(visual.gamma.createLinearRamp(rampSize=win.backend.getGammaRampSize(), driver=win.backend._driver), (3, 1))
```

### Step 5: Assign win.gamma = testGamma

```python
win.gamma = testGamma
```

### Step 6: Assign setRamp = win.backend.getGammaRamp(...)

```python
setRamp = win.backend.getGammaRamp()
```

### Step 7: Call win.close()

```python
win.close()
```

**Verification:**
```python
assert numpy.allclose(desiredRamp, setRamp, atol=1.0 / desiredRamp.shape[1])
```

### Step 8: Assign desiredRamp = value

```python
desiredRamp = desiredRamp ** (1.0 / numpy.array(testGamma))
```

### Step 9: Call win.flip()

```python
win.flip()
```


## Complete Example

```python
# Workflow
'test that the gamma ramp is set as requested'
testGamma = 2.2
win = visual.Window([600, 600], autoLog=False)
desiredRamp = numpy.tile(visual.gamma.createLinearRamp(rampSize=win.backend.getGammaRampSize(), driver=win.backend._driver), (3, 1))
if numpy.all(testGamma == 1.0) == False:
    desiredRamp = desiredRamp ** (1.0 / numpy.array(testGamma))
win.gamma = testGamma
for n in range(5):
    win.flip()
setRamp = win.backend.getGammaRamp()
win.close()
assert numpy.allclose(desiredRamp, setRamp, atol=1.0 / desiredRamp.shape[1])
```

## Next Steps


---

*Source: test_gamma.py:95 | Complexity: Advanced | Last updated: 2026-05-18*