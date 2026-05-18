# How To: Questplus

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test QuestPlus

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
conditions = data.importConditions(os.path.join(fixturesPath, 'multiStairQuestPlus.xlsx'))
```

### Step 2: Assign stairs = data.MultiStairHandler(...)

```python
stairs = data.MultiStairHandler(stairType='questplus', conditions=conditions, method='random', nTrials=20, name='QuestPlusStairs', autoLog=False)
```

### Step 3: Assign exp = data.ExperimentHandler(...)

```python
exp = data.ExperimentHandler(name='testExp', savePickle=True, saveWideText=True, dataFileName=os.path.join(self.temp_dir, 'multiQuestPlusExperiment'), autoLog=False)
```

### Step 4: Call exp.addLoop()

```python
exp.addLoop(stairs)
```

### Step 5: Call stairs.saveAsExcel()

```python
stairs.saveAsExcel(os.path.join(self.temp_dir, 'multiQuestPlusOut'))
```

### Step 6: Call stairs.saveAsPickle()

```python
stairs.saveAsPickle(os.path.join(self.temp_dir, 'multiQuestPlusOut'))
```

### Step 7: Call exp.close()

```python
exp.close()
```

### Step 8: Call pytest.skip()

```python
pytest.skip('QUEST+ only works on Python 3.6+')
```

### Step 9: Assign response = np.random.choice(...)

```python
response = np.random.choice(['Correct', 'Incorrect'])
```

### Step 10: Call stairs.addResponse()

```python
stairs.addResponse(response)
```


## Complete Example

```python
# Workflow
import sys
if not (sys.version_info.major == 3 and sys.version_info.minor >= 6):
    pytest.skip('QUEST+ only works on Python 3.6+')
conditions = data.importConditions(os.path.join(fixturesPath, 'multiStairQuestPlus.xlsx'))
stairs = data.MultiStairHandler(stairType='questplus', conditions=conditions, method='random', nTrials=20, name='QuestPlusStairs', autoLog=False)
exp = data.ExperimentHandler(name='testExp', savePickle=True, saveWideText=True, dataFileName=os.path.join(self.temp_dir, 'multiQuestPlusExperiment'), autoLog=False)
exp.addLoop(stairs)
for intensity, condition in stairs:
    response = np.random.choice(['Correct', 'Incorrect'])
    stairs.addResponse(response)
stairs.saveAsExcel(os.path.join(self.temp_dir, 'multiQuestPlusOut'))
stairs.saveAsPickle(os.path.join(self.temp_dir, 'multiQuestPlusOut'))
exp.close()
```

## Next Steps


---

*Source: test_MultiStairHandler.py:80 | Complexity: Advanced | Last updated: 2026-05-18*