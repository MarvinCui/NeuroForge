# How To: Staticperiod

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test StaticPeriod

## Prerequisites

**Required Modules:**
- `time`
- `sys`
- `numpy`
- `gc`
- `pytest`
- `psychopy`
- `psychopy.logging`
- `psychopy.tests.utils`
- `psychopy.visual`
- `psychopy.core`
- `psychopy.clock`
- `psychopy.tools`
- `traceback`
- `pprint`


## Step-by-Step Guide

### Step 1: Assign static = StaticPeriod(...)

```python
static = StaticPeriod()
```

**Verification:**
```python
assert static.complete() == 1
```

### Step 2: Call static.start()

```python
static.start(0.1)
```

**Verification:**
```python
assert static.complete() == 0
```

### Step 3: Call wait()

```python
wait(0.05)
```

**Verification:**
```python
assert win.recordFrameIntervals is False
```

### Step 4: Call static.start()

```python
static.start(0.1)
```

**Verification:**
```python
assert static._winWasRecordingIntervals == win.recordFrameIntervals
```

### Step 5: Call wait()

```python
wait(0.11)
```

**Verification:**
```python
assert np.allclose(timer.getTime(), 1.0 / refresh_rate, atol=tolerance)
```

### Step 6: Assign win = Window(...)

```python
win = Window(autoLog=False)
```

### Step 7: Assign static = StaticPeriod(...)

```python
static = StaticPeriod(screenHz=60, win=win)
```

### Step 8: Call static.start()

```python
static.start(0.002)
```

**Verification:**
```python
assert win.recordFrameIntervals is False
```

### Step 9: Call static.complete()

```python
static.complete()
```

**Verification:**
```python
assert static._winWasRecordingIntervals == win.recordFrameIntervals
```

### Step 10: Call win.close()

```python
win.close()
```

### Step 11: Assign refresh_rate = 100.0

```python
refresh_rate = 100.0
```

### Step 12: Assign period_duration = 0.1

```python
period_duration = 0.1
```

### Step 13: Assign timer = CountdownTimer(...)

```python
timer = CountdownTimer()
```

### Step 14: Assign win = Window(...)

```python
win = Window(autoLog=False)
```

### Step 15: Assign static = StaticPeriod(...)

```python
static = StaticPeriod(screenHz=refresh_rate, win=win)
```

### Step 16: Call static.start()

```python
static.start(period_duration)
```

### Step 17: Call timer.reset()

```python
timer.reset(period_duration)
```

### Step 18: Call static.complete()

```python
static.complete()
```

**Verification:**
```python
assert np.allclose(timer.getTime(), 1.0 / refresh_rate, atol=tolerance)
```

### Step 19: Call win.close()

```python
win.close()
```

### Step 20: Call pytest.skip()

```python
pytest.skip()
```

### Step 21: Assign tolerance = 0.01

```python
tolerance = 0.01
```

### Step 22: Assign tolerance = 0.001

```python
tolerance = 0.001
```


## Complete Example

```python
# Workflow
if RUNNING_IN_VM:
    pytest.skip()
static = StaticPeriod()
static.start(0.1)
wait(0.05)
assert static.complete() == 1
static.start(0.1)
wait(0.11)
assert static.complete() == 0
win = Window(autoLog=False)
static = StaticPeriod(screenHz=60, win=win)
static.start(0.002)
assert win.recordFrameIntervals is False
static.complete()
assert static._winWasRecordingIntervals == win.recordFrameIntervals
win.close()
refresh_rate = 100.0
period_duration = 0.1
timer = CountdownTimer()
win = Window(autoLog=False)
static = StaticPeriod(screenHz=refresh_rate, win=win)
static.start(period_duration)
timer.reset(period_duration)
static.complete()
if systemtools.isVM_CI():
    tolerance = 0.01
else:
    tolerance = 0.001
assert np.allclose(timer.getTime(), 1.0 / refresh_rate, atol=tolerance)
win.close()
```

## Next Steps


---

*Source: test_core.py:349 | Complexity: Advanced | Last updated: 2026-05-18*