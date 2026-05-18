# How To: Psydat Filename Collision Output

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test psydat filename collision output

## Prerequisites

**Required Modules:**
- `os`
- `glob`
- `os.path`
- `shutil`
- `tempfile`
- `numpy`
- `io`
- `pytest`
- `psychopy`
- `psychopy.tools.filetools`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: Assign conditions = value

```python
conditions = []
```

### Step 2: Assign trials = data.TrialHandler(...)

```python
trials = data.TrialHandler(trialList=conditions, seed=self.random_seed, nReps=3, method='fullRandom', autoLog=False)
```

### Step 3: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(seed=self.random_seed)
```

### Step 4: Call trials.saveAsText()

```python
trials.saveAsText(pjoin(self.temp_dir, 'testFullRandom.tsv'), stimOut=['trialType'], appendFile=False)
```

### Step 5: Call utils.compareTextFiles()

```python
utils.compareTextFiles(pjoin(self.temp_dir, 'testFullRandom.tsv'), pjoin(fixturesPath, 'corrFullRandom.tsv'))
```

### Step 6: Call trials.saveAsWideText()

```python
trials.saveAsWideText(pjoin(self.temp_dir, 'testFullRandom.csv'), delim=',', appendFile=False)
```

### Step 7: Call utils.compareTextFiles()

```python
utils.compareTextFiles(pjoin(self.temp_dir, 'testFullRandom.csv'), pjoin(fixturesPath, 'corrFullRandom.csv'))
```

### Step 8: Call conditions.append()

```python
conditions.append({'trialType': trialType})
```

### Step 9: Assign resp = value

```python
resp = 'resp' + str(thisTrial['trialType'])
```

### Step 10: Assign randResp = rng.rand(...)

```python
randResp = rng.rand()
```

### Step 11: Call trials.addData()

```python
trials.addData('resp', resp)
```

### Step 12: Call trials.addData()

```python
trials.addData('rand', randResp)
```


## Complete Example

```python
# Workflow
conditions = []
for trialType in range(5):
    conditions.append({'trialType': trialType})
trials = data.TrialHandler(trialList=conditions, seed=self.random_seed, nReps=3, method='fullRandom', autoLog=False)
rng = np.random.RandomState(seed=self.random_seed)
for thisTrial in trials:
    resp = 'resp' + str(thisTrial['trialType'])
    randResp = rng.rand()
    trials.addData('resp', resp)
    trials.addData('rand', randResp)
trials.saveAsText(pjoin(self.temp_dir, 'testFullRandom.tsv'), stimOut=['trialType'], appendFile=False)
utils.compareTextFiles(pjoin(self.temp_dir, 'testFullRandom.tsv'), pjoin(fixturesPath, 'corrFullRandom.tsv'))
trials.saveAsWideText(pjoin(self.temp_dir, 'testFullRandom.csv'), delim=',', appendFile=False)
utils.compareTextFiles(pjoin(self.temp_dir, 'testFullRandom.csv'), pjoin(fixturesPath, 'corrFullRandom.csv'))
```

## Next Steps


---

*Source: test_TrialHandler.py:108 | Complexity: Advanced | Last updated: 2026-05-18*