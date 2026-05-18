# How To: Quest

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test quest

## Prerequisites

**Required Modules:**
- `pytest`
- `shutil`
- `os`
- `numpy`
- `tempfile`
- `psychopy`
- `sys`


## Step-by-Step Guide

### Step 1: Assign conditions = data.importConditions(...)

```python
conditions = data.importConditions(os.path.join(fixturesPath, 'multiStairConds.xlsx'))
```

### Step 2: Assign stairs = data.MultiStairHandler(...)

```python
stairs = data.MultiStairHandler(stairType='quest', conditions=conditions, method='random', nTrials=20, name='QuestStairs', autoLog=False)
```

### Step 3: Assign exp = data.ExperimentHandler(...)

```python
exp = data.ExperimentHandler(name='testExp', savePickle=True, saveWideText=True, dataFileName=os.path.join(self.temp_dir, 'multiQuestExperiment'), autoLog=False)
```

### Step 4: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(seed=self.random_seed)
```

### Step 5: Call exp.addLoop()

```python
exp.addLoop(stairs)
```

### Step 6: Call stairs.saveAsExcel()

```python
stairs.saveAsExcel(os.path.join(self.temp_dir, 'multiQuestOut'))
```

### Step 7: Call stairs.saveAsPickle()

```python
stairs.saveAsPickle(os.path.join(self.temp_dir, 'multiQuestOut'))
```

### Step 8: Call exp.close()

```python
exp.close()
```

### Step 9: Call stairs.addData()

```python
stairs.addData(corr)
```

### Step 10: Assign corr = 1

```python
corr = 1
```

### Step 11: Assign corr = 0

```python
corr = 0
```


## Complete Example

```python
# Workflow
conditions = data.importConditions(os.path.join(fixturesPath, 'multiStairConds.xlsx'))
stairs = data.MultiStairHandler(stairType='quest', conditions=conditions, method='random', nTrials=20, name='QuestStairs', autoLog=False)
exp = data.ExperimentHandler(name='testExp', savePickle=True, saveWideText=True, dataFileName=os.path.join(self.temp_dir, 'multiQuestExperiment'), autoLog=False)
rng = np.random.RandomState(seed=self.random_seed)
exp.addLoop(stairs)
for intensity, condition in stairs:
    if rng.rand() > condition['startVal']:
        corr = 1
    else:
        corr = 0
    stairs.addData(corr)
stairs.saveAsExcel(os.path.join(self.temp_dir, 'multiQuestOut'))
stairs.saveAsPickle(os.path.join(self.temp_dir, 'multiQuestOut'))
exp.close()
```

## Next Steps


---

*Source: test_MultiStairHandler.py:52 | Complexity: Advanced | Last updated: 2026-05-18*