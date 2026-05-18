# How To: Find Data Dir

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test find data dir

## Prerequisites

**Required Modules:**
- `os`
- `sys`
- `tempfile`
- `os`
- `os.path`
- `tempfile`
- `pytest`
- `data`
- `test_environment`


## Step-by-Step Guide

### Step 1: Assign unknown = os.path.split(...)

```python
here, fname = os.path.split(__file__)
```

**Verification:**
```python
assert dd == here
```

### Step 2: Assign unknown = os.path.split(...)

```python
under_here, subhere = os.path.split(here)
```

**Verification:**
```python
assert dd == here
```

### Step 3: Assign dd = find_data_dir(...)

```python
dd = find_data_dir([under_here], subhere)
```

**Verification:**
```python
assert dd == here
```

### Step 4: Assign dud_dir = pjoin(...)

```python
dud_dir = pjoin(under_here, 'implausible')
```

### Step 5: Assign dd = find_data_dir(...)

```python
dd = find_data_dir([dud_dir, under_here], subhere)
```

**Verification:**
```python
assert dd == here
```

### Step 6: Call find_data_dir()

```python
find_data_dir([here], 'implausible', 'directory')
```

### Step 7: Call find_data_dir()

```python
find_data_dir([here], fname)
```


## Complete Example

```python
# Workflow
here, fname = os.path.split(__file__)
under_here, subhere = os.path.split(here)
with pytest.raises(DataError):
    find_data_dir([here], 'implausible', 'directory')
with pytest.raises(DataError):
    find_data_dir([here], fname)
dd = find_data_dir([under_here], subhere)
assert dd == here
dud_dir = pjoin(under_here, 'implausible')
dd = find_data_dir([dud_dir, under_here], subhere)
assert dd == here
```

## Next Steps


---

*Source: test_data.py:168 | Complexity: Intermediate | Last updated: 2026-05-18*