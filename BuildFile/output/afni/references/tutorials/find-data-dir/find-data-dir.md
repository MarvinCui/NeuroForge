# How To: Find Data Dir

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test find data dir

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `os.path`
- `os`
- `sys`
- `tempfile`
- `data`
- `tmpdirs`
- `nose`
- `nose.tools`
- `test_environment`


## Step-by-Step Guide

### Step 1: Assign unknown = os.path.split(...)

```python
here, fname = os.path.split(__file__)
```

### Step 2: Assign unknown = os.path.split(...)

```python
under_here, subhere = os.path.split(here)
```

### Step 3: yield (assert_raises, DataError, find_data_dir, [here], 'implausible', 'directory')

```python
yield (assert_raises, DataError, find_data_dir, [here], 'implausible', 'directory')
```

### Step 4: yield (assert_raises, DataError, find_data_dir, [here], fname)

```python
yield (assert_raises, DataError, find_data_dir, [here], fname)
```

### Step 5: Assign dd = find_data_dir(...)

```python
dd = find_data_dir([under_here], subhere)
```

### Step 6: yield (assert_equal, dd, here)

```python
yield (assert_equal, dd, here)
```

### Step 7: Assign dud_dir = pjoin(...)

```python
dud_dir = pjoin(under_here, 'implausible')
```

### Step 8: Assign dd = find_data_dir(...)

```python
dd = find_data_dir([dud_dir, under_here], subhere)
```

### Step 9: yield (assert_equal, dd, here)

```python
yield (assert_equal, dd, here)
```


## Complete Example

```python
# Workflow
here, fname = os.path.split(__file__)
under_here, subhere = os.path.split(here)
yield (assert_raises, DataError, find_data_dir, [here], 'implausible', 'directory')
yield (assert_raises, DataError, find_data_dir, [here], fname)
dd = find_data_dir([under_here], subhere)
yield (assert_equal, dd, here)
dud_dir = pjoin(under_here, 'implausible')
dd = find_data_dir([dud_dir, under_here], subhere)
yield (assert_equal, dd, here)
```

## Next Steps


---

*Source: test_data.py:185 | Complexity: Advanced | Last updated: 2026-05-18*