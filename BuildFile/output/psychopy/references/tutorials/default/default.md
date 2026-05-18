# How To: Default

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test default

## Prerequisites

**Required Modules:**
- `psychopy`
- `numpy`
- `os`
- `glob`
- `shutil`
- `io`
- `tempfile`
- `psychopy.tools.filetools`
- `pytest`


## Step-by-Step Guide

### Step 1: Assign exp = data.ExperimentHandler(...)

```python
exp = data.ExperimentHandler(name='testExp', version='0.1', extraInfo={'participant': 'jwp', 'ori': 45}, runtimeInfo=None, originPath=None, savePickle=True, saveWideText=True, dataFileName=self.tmpDir + 'default')
```

### Step 2: Assign conds = data.createFactorialTrialList(...)

```python
conds = data.createFactorialTrialList({'faceExpression': ['happy', 'sad'], 'presTime': [0.2, 0.3]})
```

### Step 3: Assign training = data.TrialHandler(...)

```python
training = data.TrialHandler(trialList=conds, nReps=3, name='train', method='random', seed=self.random_seed)
```

### Step 4: Call exp.addLoop()

```python
exp.addLoop(training)
```

### Step 5: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(seed=self.random_seed)
```

### Step 6: Assign outerLoop = data.TrialHandler(...)

```python
outerLoop = data.TrialHandler(trialList=[], nReps=3, name='stairBlock', method='random')
```

### Step 7: Call exp.addLoop()

```python
exp.addLoop(outerLoop)
```

### Step 8: Call training.addData()

```python
training.addData('training.rt', rng.rand() * 0.5 + 0.5)
```

### Step 9: Call exp.nextEntry()

```python
exp.nextEntry()
```

### Step 10: Assign staircase = data.StairHandler(...)

```python
staircase = data.StairHandler(startVal=10, name='staircase', nTrials=5)
```

### Step 11: Call exp.addLoop()

```python
exp.addLoop(staircase)
```

### Step 12: Call training.addData()

```python
training.addData('training.key', 'left')
```

### Step 13: Call training.addData()

```python
training.addData('training.key', 'right')
```

### Step 14: Assign id = rng.rand(...)

```python
id = rng.rand()
```

### Step 15: Call exp.addData()

```python
exp.addData('id', id)
```

### Step 16: Call exp.nextEntry()

```python
exp.nextEntry()
```

### Step 17: Call staircase.addData()

```python
staircase.addData(1)
```

### Step 18: Call staircase.addData()

```python
staircase.addData(0)
```


## Complete Example

```python
# Workflow
exp = data.ExperimentHandler(name='testExp', version='0.1', extraInfo={'participant': 'jwp', 'ori': 45}, runtimeInfo=None, originPath=None, savePickle=True, saveWideText=True, dataFileName=self.tmpDir + 'default')
conds = data.createFactorialTrialList({'faceExpression': ['happy', 'sad'], 'presTime': [0.2, 0.3]})
training = data.TrialHandler(trialList=conds, nReps=3, name='train', method='random', seed=self.random_seed)
exp.addLoop(training)
rng = np.random.RandomState(seed=self.random_seed)
for trial in training:
    training.addData('training.rt', rng.rand() * 0.5 + 0.5)
    if rng.rand() > 0.5:
        training.addData('training.key', 'left')
    else:
        training.addData('training.key', 'right')
    exp.nextEntry()
outerLoop = data.TrialHandler(trialList=[], nReps=3, name='stairBlock', method='random')
exp.addLoop(outerLoop)
for thisRep in outerLoop:
    staircase = data.StairHandler(startVal=10, name='staircase', nTrials=5)
    exp.addLoop(staircase)
    for thisTrial in staircase:
        id = rng.rand()
        if rng.rand() > 0.5:
            staircase.addData(1)
        else:
            staircase.addData(0)
        exp.addData('id', id)
        exp.nextEntry()
```

## Next Steps


---

*Source: test_ExperimentHandler.py:27 | Complexity: Advanced | Last updated: 2026-05-18*