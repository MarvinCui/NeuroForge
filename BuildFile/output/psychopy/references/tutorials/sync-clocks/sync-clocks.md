# How To: Sync Clocks

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that experiment clock is applied to ioHub

## Prerequisites

**Required Modules:**
- `json`
- `psychopy`
- `psychopy.hardware`
- `psychopy.tests`
- `pathlib`
- `shutil`
- `threading`
- `time`
- `psychopy`
- `psychopy`


## Step-by-Step Guide

### Step 1: '\n        Test that experiment clock is applied to ioHub\n        '

```python
'\n        Test that experiment clock is applied to ioHub\n        '
```

**Verification:**
```python
assert _sameTimes(), (deviceManager.ioServer.getTime(), iohub.Computer.global_clock.getTime(), self.sess.sessionClock.getTime())
```

### Step 2: Call time.sleep()

```python
time.sleep(1)
```

### Step 3: Call self.sess.runExperiment()

```python
self.sess.runExperiment('exp1')
```

**Verification:**
```python
assert _sameTimes(), (deviceManager.ioServer.getTime(), iohub.Computer.global_clock.getTime(), self.sess.sessionClock.getTime())
```

### Step 4: Assign times = value

```python
times = [deviceManager.ioServer.getTime(), iohub.Computer.global_clock.getTime(), self.sess.sessionClock.getTime()]
```

### Step 5: Assign avg = value

```python
avg = sum(times) / len(times)
```

### Step 6: Assign deltas = value

```python
deltas = [abs(t - avg) for t in times]
```

### Step 7: Assign same = value

```python
same = [d < 0.001 for d in deltas]
```


## Complete Example

```python
# Workflow
'\n        Test that experiment clock is applied to ioHub\n        '
from psychopy import iohub

def _sameTimes():
    times = [deviceManager.ioServer.getTime(), iohub.Computer.global_clock.getTime(), self.sess.sessionClock.getTime()]
    avg = sum(times) / len(times)
    deltas = [abs(t - avg) for t in times]
    same = [d < 0.001 for d in deltas]
    return all(same)
time.sleep(1)
self.sess.runExperiment('exp1')
assert _sameTimes(), (deviceManager.ioServer.getTime(), iohub.Computer.global_clock.getTime(), self.sess.sessionClock.getTime())
```

## Next Steps


---

*Source: test_Session.py:81 | Complexity: Intermediate | Last updated: 2026-05-18*