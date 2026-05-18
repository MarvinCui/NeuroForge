# How To: Output Csv Suffix No Delim

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test output csv suffix no delim

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

### Step 1: Assign unknown = mkstemp(...)

```python
_, path = mkstemp(dir=self.temp_dir, suffix='.csv')
```

**Verification:**
```python
assert header == expected_header
```

### Step 2: Assign delim = None

```python
delim = None
```

### Step 3: Call self.trials.saveAsWideText()

```python
self.trials.saveAsWideText(path, delim=delim)
```

### Step 4: Assign expected_delim = ','

```python
expected_delim = ','
```

### Step 5: Assign expected_header = value

```python
expected_header = ['TrialNumber']
```

### Step 6: Call expected_header.extend()

```python
expected_header.extend(list(self.trials.trialList[0].keys()))
```

### Step 7: Call expected_header.extend()

```python
expected_header.extend(self.trials.data.dataTypes)
```

### Step 8: Assign expected_header = value

```python
expected_header = expected_delim.join(expected_header) + '\n'
```

**Verification:**
```python
assert header == expected_header
```

### Step 9: Assign header = f.readline(...)

```python
header = f.readline()
```


## Complete Example

```python
# Workflow
_, path = mkstemp(dir=self.temp_dir, suffix='.csv')
delim = None
self.trials.saveAsWideText(path, delim=delim)
expected_delim = ','
expected_header = ['TrialNumber']
expected_header.extend(list(self.trials.trialList[0].keys()))
expected_header.extend(self.trials.data.dataTypes)
expected_header = expected_delim.join(expected_header) + '\n'
with io.open(path, 'r', encoding='utf-8-sig') as f:
    header = f.readline()
assert header == expected_header
```

## Next Steps


---

*Source: test_TrialHandler.py:280 | Complexity: Advanced | Last updated: 2026-05-18*