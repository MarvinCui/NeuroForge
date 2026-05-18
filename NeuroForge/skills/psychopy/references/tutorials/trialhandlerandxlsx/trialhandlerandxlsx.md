# How To: Trialhandlerandxlsx

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Currently tests the contents of xslx file against known good example
        

## Prerequisites

**Required Modules:**
- `os`
- `shutil`
- `numpy`
- `tempfile`
- `pytest`
- `psychopy`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: 'Currently tests the contents of xslx file against known good example\n        '

```python
'Currently tests the contents of xslx file against known good example\n        '
```

**Verification:**
```python
assert os.path.isfile(self.fullName)
```

### Step 2: Assign conds = data.importConditions(...)

```python
conds = data.importConditions(os.path.join(fixturesPath, 'trialTypes.xlsx'))
```

### Step 3: Assign trials = data.TrialHandler(...)

```python
trials = data.TrialHandler(trialList=conds, seed=self.random_seed, nReps=2, autoLog=False)
```

### Step 4: Assign responses = value

```python
responses = [1, 1, None, 3, 2, 3, 1, 3, 2, 2, 1, 1]
```

### Step 5: Assign rts = value

```python
rts = [0.1, 0.1, None, 0.3, 0.2, 0.3, 0.1, 0.3, 0.2, 0.2, 0.1, 0.1]
```

### Step 6: Call trials.saveAsExcel()

```python
trials.saveAsExcel(self.name)
```

### Step 7: Call trials.saveAsText()

```python
trials.saveAsText(self.name, delim=',')
```

### Step 8: Call trials.saveAsWideText()

```python
trials.saveAsWideText(os.path.join(self.temp_dir, 'actualXlsx'))
```

**Verification:**
```python
assert os.path.isfile(self.fullName)
```

### Step 9: Call utils.compareXlsxFiles()

```python
utils.compareXlsxFiles(self.fullName, os.path.join(fixturesPath, 'corrXlsx.xlsx'))
```

### Step 10: Call trials.addData()

```python
trials.addData('resp', responses[trialN])
```

### Step 11: Call trials.addData()

```python
trials.addData('rt', rts[trialN])
```


## Complete Example

```python
# Workflow
'Currently tests the contents of xslx file against known good example\n        '
conds = data.importConditions(os.path.join(fixturesPath, 'trialTypes.xlsx'))
trials = data.TrialHandler(trialList=conds, seed=self.random_seed, nReps=2, autoLog=False)
responses = [1, 1, None, 3, 2, 3, 1, 3, 2, 2, 1, 1]
rts = [0.1, 0.1, None, 0.3, 0.2, 0.3, 0.1, 0.3, 0.2, 0.2, 0.1, 0.1]
for trialN, trial in enumerate(trials):
    if responses[trialN] is None:
        continue
    trials.addData('resp', responses[trialN])
    trials.addData('rt', rts[trialN])
trials.saveAsExcel(self.name)
trials.saveAsText(self.name, delim=',')
trials.saveAsWideText(os.path.join(self.temp_dir, 'actualXlsx'))
assert os.path.isfile(self.fullName)
utils.compareXlsxFiles(self.fullName, os.path.join(fixturesPath, 'corrXlsx.xlsx'))
```

## Next Steps


---

*Source: test_xlsx.py:25 | Complexity: Advanced | Last updated: 2026-05-18*