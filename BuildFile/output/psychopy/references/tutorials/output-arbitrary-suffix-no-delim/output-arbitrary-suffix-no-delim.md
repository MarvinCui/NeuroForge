# How To: Output Arbitrary Suffix No Delim

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test output arbitrary suffix no delim

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
_, path = mkstemp(dir=self.temp_dir, suffix='.xyz')
```

**Verification:**
```python
assert os.path.isfile(path + expected_suffix)
```

### Step 2: Assign delim = None

```python
delim = None
```

**Verification:**
```python
assert header == expected_header
```

### Step 3: Call self.trials.saveAsWideText()

```python
self.trials.saveAsWideText(path, delim=delim)
```

### Step 4: Assign expected_suffix = '.tsv'

```python
expected_suffix = '.tsv'
```

**Verification:**
```python
assert os.path.isfile(path + expected_suffix)
```

### Step 5: Assign expected_delim = '\t'

```python
expected_delim = '\t'
```

### Step 6: Assign expected_header = value

```python
expected_header = ['TrialNumber']
```

### Step 7: Call expected_header.extend()

```python
expected_header.extend(list(self.trials.trialList[0].keys()))
```

### Step 8: Call expected_header.extend()

```python
expected_header.extend(self.trials.data.dataTypes)
```

### Step 9: Assign expected_header = value

```python
expected_header = expected_delim.join(expected_header) + '\n'
```

**Verification:**
```python
assert header == expected_header
```

### Step 10: Assign header = f.readline(...)

```python
header = f.readline()
```


## Complete Example

```python
# Workflow
_, path = mkstemp(dir=self.temp_dir, suffix='.xyz')
delim = None
self.trials.saveAsWideText(path, delim=delim)
expected_suffix = '.tsv'
assert os.path.isfile(path + expected_suffix)
expected_delim = '\t'
expected_header = ['TrialNumber']
expected_header.extend(list(self.trials.trialList[0].keys()))
expected_header.extend(self.trials.data.dataTypes)
expected_header = expected_delim.join(expected_header) + '\n'
with io.open(path + expected_suffix, 'r', encoding='utf-8-sig') as f:
    header = f.readline()
assert header == expected_header
```

## Next Steps


---

*Source: test_TrialHandler.py:296 | Complexity: Advanced | Last updated: 2026-05-18*