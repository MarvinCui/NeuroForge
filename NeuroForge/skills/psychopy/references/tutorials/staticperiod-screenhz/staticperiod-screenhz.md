# How To: Staticperiod Screenhz

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if screenHz parameter is respected, i.e., if after completion of the
StaticPeriod, 1/screenHz seconds are still remaining, so the period will
complete after the next flip.

## Prerequisites

**Required Modules:**
- `numpy`
- `psychopy.clock`
- `psychopy.visual`
- `psychopy.tools`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: 'Test if screenHz parameter is respected, i.e., if after completion of the\n    StaticPeriod, 1/screenHz seconds are still remaining, so the period will\n    complete after the next flip.\n    '

```python
'Test if screenHz parameter is respected, i.e., if after completion of the\n    StaticPeriod, 1/screenHz seconds are still remaining, so the period will\n    complete after the next flip.\n    '
```

**Verification:**
```python
assert np.allclose(timer.getTime(), 1.0 / refresh_rate, atol=tolerance)
```

### Step 2: Assign refresh_rate = 100.0

```python
refresh_rate = 100.0
```

### Step 3: Assign period_duration = 0.1

```python
period_duration = 0.1
```

### Step 4: Assign timer = CountdownTimer(...)

```python
timer = CountdownTimer()
```

### Step 5: Assign win = Window(...)

```python
win = Window(autoLog=False)
```

### Step 6: Assign static = StaticPeriod(...)

```python
static = StaticPeriod(screenHz=refresh_rate, win=win)
```

### Step 7: Call static.start()

```python
static.start(period_duration)
```

### Step 8: Call timer.reset()

```python
timer.reset(period_duration)
```

### Step 9: Call static.complete()

```python
static.complete()
```

**Verification:**
```python
assert np.allclose(timer.getTime(), 1.0 / refresh_rate, atol=tolerance)
```

### Step 10: Call win.close()

```python
win.close()
```

### Step 11: Assign tolerance = 0.01

```python
tolerance = 0.01
```

### Step 12: Assign tolerance = 0.001

```python
tolerance = 0.001
```


## Complete Example

```python
# Workflow
'Test if screenHz parameter is respected, i.e., if after completion of the\n    StaticPeriod, 1/screenHz seconds are still remaining, so the period will\n    complete after the next flip.\n    '
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

*Source: test_clock.py:41 | Complexity: Advanced | Last updated: 2026-05-18*