# How To: Trialtypeimport

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test TrialTypeImport

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

### Step 1: Assign fromCSV = data.importConditions(...)

```python
fromCSV = data.importConditions(os.path.join(fixturesPath, 'trialTypes.csv'))
```

**Verification:**
```python
assert list(trialXLSX.keys()) == list(trialCSV.keys())
```

### Step 2: Assign fromXLSX = data.importConditions(...)

```python
fromXLSX = data.importConditions(os.path.join(fixturesPath, 'trialTypes.xlsx'))
```

**Verification:**
```python
assert trialXLSX[header] == trialCSV[header]
```

### Step 3: Call checkEachtrial()

```python
checkEachtrial(fromCSV, fromXLSX)
```

### Step 4: Assign haveXlrd = value

```python
haveXlrd = data.haveXlrd
```

### Step 5: Assign data.haveXlrd = False

```python
data.haveXlrd = False
```

### Step 6: Assign fromXLSX = data.importConditions(...)

```python
fromXLSX = data.importConditions(os.path.join(fixturesPath, 'trialTypes.xlsx'))
```

### Step 7: Call checkEachtrial()

```python
checkEachtrial(fromCSV, fromXLSX)
```

### Step 8: Assign data.haveXlrd = haveXlrd

```python
data.haveXlrd = haveXlrd
```

### Step 9: Assign trialXLSX = value

```python
trialXLSX = fromXLSX[trialN]
```

**Verification:**
```python
assert list(trialXLSX.keys()) == list(trialCSV.keys())
```

### Step 10: Call print()

```python
print(header, trialCSV[header], trialXLSX[header])
```


## Complete Example

```python
# Workflow
def checkEachtrial(fromCSV, fromXLSX):
    for trialN, trialCSV in enumerate(fromCSV):
        trialXLSX = fromXLSX[trialN]
        assert list(trialXLSX.keys()) == list(trialCSV.keys())
        for header in trialCSV:
            if trialXLSX[header] != trialCSV[header]:
                print(header, trialCSV[header], trialXLSX[header])
            assert trialXLSX[header] == trialCSV[header]
fromCSV = data.importConditions(os.path.join(fixturesPath, 'trialTypes.csv'))
fromXLSX = data.importConditions(os.path.join(fixturesPath, 'trialTypes.xlsx'))
checkEachtrial(fromCSV, fromXLSX)
haveXlrd = data.haveXlrd
data.haveXlrd = False
fromXLSX = data.importConditions(os.path.join(fixturesPath, 'trialTypes.xlsx'))
checkEachtrial(fromCSV, fromXLSX)
data.haveXlrd = haveXlrd
```

## Next Steps


---

*Source: test_xlsx.py:53 | Complexity: Advanced | Last updated: 2026-05-18*