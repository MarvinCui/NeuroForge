# How To: Stairhandlerscalarstepsize

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test StairHandlerScalarStepSize

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

### Step 2: Assign unknown = value

```python
startVal, minVal, maxVal = (0.8, 0, 1)
```

### Step 3: Assign stepSizes = 0.1

```python
stepSizes = 0.1
```

### Step 4: Assign unknown = value

```python
nUp, nDown = (1, 1)
```

### Step 5: Assign nReversals = 6

```python
nReversals = 6
```

### Step 6: Assign stepType = 'lin'

```python
stepType = 'lin'
```

### Step 7: Assign self.stairs = data.StairHandler(...)

```python
self.stairs = data.StairHandler(startVal=startVal, nUp=nUp, nDown=nDown, minVal=minVal, maxVal=maxVal, nReversals=nReversals, stepSizes=stepSizes, nTrials=nTrials, stepType=stepType)
```

### Step 8: Assign self.responses = makeBasicResponseCycles(...)

```python
self.responses = makeBasicResponseCycles(cycles=4, nCorrect=2, nIncorrect=1, length=10)
```

### Step 9: Assign self.intensities = value

```python
self.intensities = [0.8, 0.7, 0.6, 0.7, 0.6, 0.5, 0.6, 0.5, 0.4, 0.5]
```

### Step 10: Assign self.reversalPoints = value

```python
self.reversalPoints = [2, 3, 5, 6, 8, 9]
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
nTrials = 10
startVal, minVal, maxVal = (0.8, 0, 1)
stepSizes = 0.1
nUp, nDown = (1, 1)
nReversals = 6
stepType = 'lin'
self.stairs = data.StairHandler(startVal=startVal, nUp=nUp, nDown=nDown, minVal=minVal, maxVal=maxVal, nReversals=nReversals, stepSizes=stepSizes, nTrials=nTrials, stepType=stepType)
self.responses = makeBasicResponseCycles(cycles=4, nCorrect=2, nIncorrect=1, length=10)
self.intensities = [0.8, 0.7, 0.6, 0.7, 0.6, 0.5, 0.6, 0.5, 0.4, 0.5]
self.reversalPoints = [2, 3, 5, 6, 8, 9]
self.reversalIntensities = list(itemgetter(*self.reversalPoints)(self.intensities))
self.simulate()
self.checkSimulationResults()
```

## Next Steps


---

*Source: test_StairHandlers.py:223 | Complexity: Advanced | Last updated: 2026-05-18*