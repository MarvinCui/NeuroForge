# How To: Stairhandlerlog

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test StairHandlerLog

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

### Step 1: Assign nTrials = 20

```python
nTrials = 20
```

### Step 2: Assign unknown = value

```python
startVal, minVal, maxVal = (0.8, 0, 1)
```

### Step 3: Assign stepSizes = value

```python
stepSizes = [0.4 / 20, 0.2 / 20, 0.2 / 20, 0.1 / 20]
```

### Step 4: Assign unknown = value

```python
nUp, nDown = (1, 3)
```

### Step 5: Assign nReversals = 4

```python
nReversals = 4
```

### Step 6: Assign stepType = 'log'

```python
stepType = 'log'
```

### Step 7: Assign self.stairs = data.StairHandler(...)

```python
self.stairs = data.StairHandler(startVal=startVal, nUp=nUp, nDown=nDown, minVal=minVal, maxVal=maxVal, nReversals=nReversals, stepSizes=stepSizes, nTrials=nTrials, stepType=stepType)
```

### Step 8: Assign self.responses = makeBasicResponseCycles(...)

```python
self.responses = makeBasicResponseCycles(cycles=3, nCorrect=4, nIncorrect=4, length=20)
```

### Step 9: Assign self.intensities = value

```python
self.intensities = [0.8, 0.763994069, 0.729608671, 0.696770872, 0.665411017, 0.680910431, 0.696770872, 0.713000751, 0.729608671, 0.729608671, 0.729608671, 0.713000751, 0.713000751, 0.72125691, 0.729608671, 0.738057142, 0.746603441, 0.746603441, 0.746603441, 0.738057142]
```

### Step 10: Assign self.reversalPoints = value

```python
self.reversalPoints = [4, 10, 12, 18]
```

### Step 11: Assign self.reversalIntensities = list(...)

```python
self.reversalIntensities = list(itemgetter(*self.reversalPoints)(self.intensities))
```

### Step 12: Call self.simulate()

```python
self.simulate()
```

### Step 13: Call self.checkSimulationResults()

```python
self.checkSimulationResults()
```


## Complete Example

```python
# Workflow
nTrials = 20
startVal, minVal, maxVal = (0.8, 0, 1)
stepSizes = [0.4 / 20, 0.2 / 20, 0.2 / 20, 0.1 / 20]
nUp, nDown = (1, 3)
nReversals = 4
stepType = 'log'
self.stairs = data.StairHandler(startVal=startVal, nUp=nUp, nDown=nDown, minVal=minVal, maxVal=maxVal, nReversals=nReversals, stepSizes=stepSizes, nTrials=nTrials, stepType=stepType)
self.responses = makeBasicResponseCycles(cycles=3, nCorrect=4, nIncorrect=4, length=20)
self.intensities = [0.8, 0.763994069, 0.729608671, 0.696770872, 0.665411017, 0.680910431, 0.696770872, 0.713000751, 0.729608671, 0.729608671, 0.729608671, 0.713000751, 0.713000751, 0.72125691, 0.729608671, 0.738057142, 0.746603441, 0.746603441, 0.746603441, 0.738057142]
self.reversalPoints = [4, 10, 12, 18]
self.reversalIntensities = list(itemgetter(*self.reversalPoints)(self.intensities))
self.simulate()
self.checkSimulationResults()
```

## Next Steps


---

*Source: test_StairHandlers.py:154 | Complexity: Advanced | Last updated: 2026-05-18*