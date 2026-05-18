# How To: Adddata With Mutable Values

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test addData with mutable values

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
exp = data.ExperimentHandler(name='testExp', savePickle=False, saveWideText=True, dataFileName=self.tmpDir + 'mutables')
```

**Verification:**
```python
assert contents == 'thisRow.t,notes,mutable,\n,,[1],\n,,[9999],\n'
```

### Step 2: Assign mutant = value

```python
mutant = [1]
```

### Step 3: Call exp.addData()

```python
exp.addData('mutable', mutant)
```

### Step 4: Call exp.nextEntry()

```python
exp.nextEntry()
```

### Step 5: Assign unknown = 9999

```python
mutant[0] = 9999
```

### Step 6: Call exp.addData()

```python
exp.addData('mutable', mutant)
```

### Step 7: Call exp.nextEntry()

```python
exp.nextEntry()
```

### Step 8: Call exp.saveAsWideText()

```python
exp.saveAsWideText(exp.dataFileName + '.csv', delim=',')
```

**Verification:**
```python
assert contents == 'thisRow.t,notes,mutable,\n,,[1],\n,,[9999],\n'
```

### Step 9: Assign contents = f.read(...)

```python
contents = f.read()
```


## Complete Example

```python
# Workflow
exp = data.ExperimentHandler(name='testExp', savePickle=False, saveWideText=True, dataFileName=self.tmpDir + 'mutables')
mutant = [1]
exp.addData('mutable', mutant)
exp.nextEntry()
mutant[0] = 9999
exp.addData('mutable', mutant)
exp.nextEntry()
exp.saveAsWideText(exp.dataFileName + '.csv', delim=',')
with io.open(exp.dataFileName + '.csv', 'r', encoding='utf-8-sig') as f:
    contents = f.read()
assert contents == 'thisRow.t,notes,mutable,\n,,[1],\n,,[9999],\n'
```

## Next Steps


---

*Source: test_ExperimentHandler.py:80 | Complexity: Advanced | Last updated: 2026-05-18*