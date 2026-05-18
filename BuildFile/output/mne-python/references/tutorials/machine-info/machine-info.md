# How To: Machine Info

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading the machine info.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.io.ant.ant`

**Setup Required:**
```python
# Fixtures: dataset, request
```

## Step-by-Step Guide

### Step 1: 'Test reading the machine info.'

```python
'Test reading the machine info.'
```

**Verification:**
```python
assert device_info['type'] == make
```

### Step 2: Assign dataset = request.getfixturevalue(...)

```python
dataset = request.getfixturevalue(dataset)
```

**Verification:**
```python
assert device_info['model'] == model
```

### Step 3: Assign raw_cnt = read_raw_ant(...)

```python
raw_cnt = read_raw_ant(dataset['cnt']['short'])
```

**Verification:**
```python
assert device_info['serial'] == serial
```

### Step 4: Assign device_info = value

```python
device_info = raw_cnt.info['device_info']
```

### Step 5: Assign unknown = value

```python
make, model, serial = dataset['machine_info']
```

**Verification:**
```python
assert device_info['type'] == make
```


## Complete Example

```python
# Setup
# Fixtures: dataset, request

# Workflow
'Test reading the machine info.'
dataset = request.getfixturevalue(dataset)
raw_cnt = read_raw_ant(dataset['cnt']['short'])
device_info = raw_cnt.info['device_info']
make, model, serial = dataset['machine_info']
assert device_info['type'] == make
assert device_info['model'] == model
assert device_info['serial'] == serial
```

## Next Steps


---

*Source: test_ant.py:347 | Complexity: Intermediate | Last updated: 2026-05-18*