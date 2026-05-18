# How To: Psydat Filename Collision Output2

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test psydat filename collision output2

## Prerequisites

**Required Modules:**
- `os`
- `glob`
- `os.path`
- `shutil`
- `tempfile`
- `numpy`
- `io`
- `json_tricks`
- `pytest`
- `psychopy`
- `psychopy.tools.filetools`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: Assign conditions = value

```python
conditions = []
```

### Step 2: Assign trials = data.TrialHandler2(...)

```python
trials = data.TrialHandler2(trialList=conditions, seed=self.random_seed, nReps=3, method='fullRandom', autoLog=False)
```

### Step 3: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(seed=self.random_seed)
```

### Step 4: Call trials.saveAsWideText()

```python
trials.saveAsWideText(pjoin(self.temp_dir, 'testFullRandom.csv'), delim=',', appendFile=False)
```

### Step 5: Call utils.compareTextFiles()

```python
utils.compareTextFiles(pjoin(self.temp_dir, 'testFullRandom.csv'), pjoin(fixturesPath, 'corrFullRandomTH2.csv'))
```

### Step 6: Call conditions.append()

```python
conditions.append({'trialType': trialType})
```

### Step 7: Assign resp = value

```python
resp = 'resp' + str(thisTrial['trialType'])
```

### Step 8: Assign randResp = rng.rand(...)

```python
randResp = rng.rand()
```

### Step 9: Call trials.addData()

```python
trials.addData('resp', resp)
```

### Step 10: Call trials.addData()

```python
trials.addData('rand', randResp)
```


## Complete Example

```python
# Workflow
conditions = []
for trialType in range(5):
    conditions.append({'trialType': trialType})
trials = data.TrialHandler2(trialList=conditions, seed=self.random_seed, nReps=3, method='fullRandom', autoLog=False)
rng = np.random.RandomState(seed=self.random_seed)
for thisTrial in trials:
    resp = 'resp' + str(thisTrial['trialType'])
    randResp = rng.rand()
    trials.addData('resp', resp)
    trials.addData('rand', randResp)
trials.saveAsWideText(pjoin(self.temp_dir, 'testFullRandom.csv'), delim=',', appendFile=False)
utils.compareTextFiles(pjoin(self.temp_dir, 'testFullRandom.csv'), pjoin(fixturesPath, 'corrFullRandomTH2.csv'))
```

## Next Steps


---

*Source: test_TrialHandler2.py:124 | Complexity: Advanced | Last updated: 2026-05-18*