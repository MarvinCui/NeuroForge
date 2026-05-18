# How To: Questhandler

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test QuestHandler

## Prerequisites

**Required Modules:**
- `numpy`
- `shutil`
- `json_tricks`
- `tempfile`
- `operator`
- `pytest`
- `psychopy`
- `psychopy.tools.filetools`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`


## Step-by-Step Guide

### Step 1: Assign nTrials = 10

```python
nTrials = 10
```

**Verification:**
```python
assert self.stairs.startVal == startVal
```

### Step 2: Assign unknown = value

```python
startVal, minVal, maxVal = (50, 0, 100)
```

**Verification:**
```python
assert self.stairs.startValSd == startValSd
```

### Step 3: Assign range = value

```python
range = maxVal - minVal
```

**Verification:**
```python
assert np.allclose(self.stairs.mean(), mean)
```

### Step 4: Assign startValSd = 50

```python
startValSd = 50
```

**Verification:**
```python
assert np.allclose(self.stairs.mode(), mode)
```

### Step 5: Assign grain = 0.01

```python
grain = 0.01
```

**Verification:**
```python
assert np.allclose(self.stairs.quantile(), quantile)
```

### Step 6: Assign pThreshold = 0.82

```python
pThreshold = 0.82
```

**Verification:**
```python
assert len(self.stairs._quest.x) == (maxVal - minVal) / grain + 1
```

### Step 7: Assign unknown = value

```python
beta, gamma, delta = (3.5, 0.5, 0.01)
```

**Verification:**
```python
assert np.allclose(self.stairs._quest.x[1] - self.stairs._quest.x[0], grain)
```

### Step 8: Assign stopInterval = None

```python
stopInterval = None
```

**Verification:**
```python
assert self.stairs._quest.x[0] == -range / 2
```

### Step 9: Assign method = 'quantile'

```python
method = 'quantile'
```

**Verification:**
```python
assert self.stairs._quest.x[-1] == range / 2
```

### Step 10: Assign self.stairs = data.QuestHandler(...)

```python
self.stairs = data.QuestHandler(startVal, startValSd, pThreshold=pThreshold, nTrials=nTrials, stopInterval=stopInterval, method=method, beta=beta, gamma=gamma, delta=delta, grain=grain, range=range, minVal=minVal, maxVal=maxVal)
```

### Step 11: Assign self.stairs.nReversals = None

```python
self.stairs.nReversals = None
```

### Step 12: Assign self.responses = makeBasicResponseCycles(...)

```python
self.responses = makeBasicResponseCycles(cycles=3, nCorrect=2, nIncorrect=2, length=10)
```

### Step 13: Assign self.intensities = value

```python
self.intensities = [50, 45.13971040707487, 37.29108650393074, 58.29741312713995, 80.18296713109655, 75.29525140900353, 71.57627192423783, 79.8816804840369, 90.71231330281552, 88.2658089576958]
```

### Step 14: Assign mean = 86.0772169427

```python
mean = 86.0772169427
```

### Step 15: Assign mode = 80.11

```python
mode = 80.11
```

### Step 16: Assign quantile = 86.3849031085

```python
quantile = 86.3849031085
```

### Step 17: Call self.simulate()

```python
self.simulate()
```

### Step 18: Call self.checkSimulationResults()

```python
self.checkSimulationResults()
```

**Verification:**
```python
assert self.stairs.startVal == startVal
```


## Complete Example

```python
# Workflow
nTrials = 10
startVal, minVal, maxVal = (50, 0, 100)
range = maxVal - minVal
startValSd = 50
grain = 0.01
pThreshold = 0.82
beta, gamma, delta = (3.5, 0.5, 0.01)
stopInterval = None
method = 'quantile'
self.stairs = data.QuestHandler(startVal, startValSd, pThreshold=pThreshold, nTrials=nTrials, stopInterval=stopInterval, method=method, beta=beta, gamma=gamma, delta=delta, grain=grain, range=range, minVal=minVal, maxVal=maxVal)
self.stairs.nReversals = None
self.responses = makeBasicResponseCycles(cycles=3, nCorrect=2, nIncorrect=2, length=10)
self.intensities = [50, 45.13971040707487, 37.29108650393074, 58.29741312713995, 80.18296713109655, 75.29525140900353, 71.57627192423783, 79.8816804840369, 90.71231330281552, 88.2658089576958]
mean = 86.0772169427
mode = 80.11
quantile = 86.3849031085
self.simulate()
self.checkSimulationResults()
assert self.stairs.startVal == startVal
assert self.stairs.startValSd == startValSd
assert np.allclose(self.stairs.mean(), mean)
assert np.allclose(self.stairs.mode(), mode)
assert np.allclose(self.stairs.quantile(), quantile)
assert len(self.stairs._quest.x) == (maxVal - minVal) / grain + 1
assert np.allclose(self.stairs._quest.x[1] - self.stairs._quest.x[0], grain)
assert self.stairs._quest.x[0] == -range / 2
assert self.stairs._quest.x[-1] == range / 2
```

## Next Steps


---

*Source: test_StairHandlers.py:452 | Complexity: Advanced | Last updated: 2026-05-18*