# How To: Underscores In Datatype Names2

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test underscores in datatype names2

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

### Step 1: Assign trials = data.TrialHandler2(...)

```python
trials = data.TrialHandler2([], 1, autoLog=False)
```

**Verification:**
```python
assert os.path.exists(data_filename), 'File not found: %s' % os.path.abspath(data_filename)
```

### Step 2: Assign base_data_filename = pjoin(...)

```python
base_data_filename = pjoin(self.temp_dir, self.rootName)
```

### Step 3: Assign data_filename = value

```python
data_filename = base_data_filename + '.csv'
```

### Step 4: Call trials.saveAsWideText()

```python
trials.saveAsWideText(data_filename, delim=',', appendFile=False)
```

**Verification:**
```python
assert os.path.exists(data_filename), 'File not found: %s' % os.path.abspath(data_filename)
```

### Step 5: Assign expected_header = 'n,with_underscore_mean,with_underscore_raw,with_underscore_std,order\n'

```python
expected_header = u'n,with_underscore_mean,with_underscore_raw,with_underscore_std,order\n'
```

### Step 6: Call trials.addData()

```python
trials.addData('with_underscore', 0)
```

### Step 7: Assign header = f.readline(...)

```python
header = f.readline()
```

### Step 8: Call print()

```python
print(base_data_filename)
```

### Step 9: Call print()

```python
print(repr(expected_header), type(expected_header), len(expected_header))
```

### Step 10: Call print()

```python
print(repr(header), type(header), len(header))
```


## Complete Example

```python
# Workflow
trials = data.TrialHandler2([], 1, autoLog=False)
for trial in trials:
    trials.addData('with_underscore', 0)
base_data_filename = pjoin(self.temp_dir, self.rootName)
data_filename = base_data_filename + '.csv'
trials.saveAsWideText(data_filename, delim=',', appendFile=False)
assert os.path.exists(data_filename), 'File not found: %s' % os.path.abspath(data_filename)
with io.open(data_filename, 'r', encoding='utf-8-sig') as f:
    header = f.readline()
expected_header = u'n,with_underscore_mean,with_underscore_raw,with_underscore_std,order\n'
if expected_header != header:
    print(base_data_filename)
    print(repr(expected_header), type(expected_header), len(expected_header))
    print(repr(header), type(header), len(header))
```

## Next Steps


---

*Source: test_TrialHandler2.py:52 | Complexity: Advanced | Last updated: 2026-05-18*