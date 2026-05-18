# How To: Underscores In Datatype Names

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test underscores in datatype names

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

### Step 1: Assign trials = data.TrialHandler(...)

```python
trials = data.TrialHandler([], 1, autoLog=False)
```

**Verification:**
```python
assert os.path.exists(data_filename), 'File not found: %s' % os.path.abspath(data_filename)
```

### Step 2: Call trials.data.addDataType()

```python
trials.data.addDataType('with_underscore')
```

**Verification:**
```python
assert expected_header == str(header)
```

### Step 3: Assign base_data_filename = pjoin(...)

```python
base_data_filename = pjoin(self.temp_dir, self.rootName)
```

### Step 4: Call trials.saveAsExcel()

```python
trials.saveAsExcel(base_data_filename)
```

### Step 5: Call trials.saveAsText()

```python
trials.saveAsText(base_data_filename, delim=',')
```

### Step 6: Assign data_filename = value

```python
data_filename = base_data_filename + '.csv'
```

**Verification:**
```python
assert os.path.exists(data_filename), 'File not found: %s' % os.path.abspath(data_filename)
```

### Step 7: Assign expected_header = 'n,with_underscore_mean,with_underscore_raw,with_underscore_std,order\n'

```python
expected_header = u'n,with_underscore_mean,with_underscore_raw,with_underscore_std,order\n'
```

**Verification:**
```python
assert expected_header == str(header)
```

### Step 8: Call trials.addData()

```python
trials.addData('with_underscore', 0)
```

### Step 9: Assign header = f.readline(...)

```python
header = f.readline()
```

### Step 10: Call print()

```python
print(base_data_filename)
```

### Step 11: Call print()

```python
print(repr(expected_header), type(expected_header), len(expected_header))
```

### Step 12: Call print()

```python
print(repr(header), type(header), len(header))
```


## Complete Example

```python
# Workflow
trials = data.TrialHandler([], 1, autoLog=False)
trials.data.addDataType('with_underscore')
for trial in trials:
    trials.addData('with_underscore', 0)
base_data_filename = pjoin(self.temp_dir, self.rootName)
trials.saveAsExcel(base_data_filename)
trials.saveAsText(base_data_filename, delim=',')
data_filename = base_data_filename + '.csv'
assert os.path.exists(data_filename), 'File not found: %s' % os.path.abspath(data_filename)
with io.open(data_filename, 'r', encoding='utf-8-sig') as f:
    header = f.readline()
expected_header = u'n,with_underscore_mean,with_underscore_raw,with_underscore_std,order\n'
if expected_header != header:
    print(base_data_filename)
    print(repr(expected_header), type(expected_header), len(expected_header))
    print(repr(header), type(header), len(header))
assert expected_header == str(header)
```

## Next Steps


---

*Source: test_TrialHandler.py:28 | Complexity: Advanced | Last updated: 2026-05-18*