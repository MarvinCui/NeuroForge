# How To: Morph Data

**Difficulty**: Advanced
**Estimated Time**: 10 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: Test IO of morphometry data file (eg. curvature).

## Prerequisites

**Required Modules:**
- `getpass`
- `hashlib`
- `os`
- `struct`
- `time`
- `unittest`
- `os.path`
- `os.path`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileslice`
- `testing`
- `tests.nibabel_data`
- `tmpdirs`
- `io`


## Step-by-Step Guide

### Step 1: 'Test IO of morphometry data file (eg. curvature).'

```python
'Test IO of morphometry data file (eg. curvature).'
```

**Verification:**
```python
assert -1.0 < curv.min() < 0
```

### Step 2: Assign curv_path = pjoin(...)

```python
curv_path = pjoin(data_path, 'surf', 'lh.curv')
```

**Verification:**
```python
assert 0 < curv.max() < 1.0
```

### Step 3: Assign curv = read_morph_data(...)

```python
curv = read_morph_data(curv_path)
```

**Verification:**
```python
assert np.array_equal(curv2, curv)
```

### Step 4: Assign new_path = 'test'

```python
new_path = 'test'
```

### Step 5: Call write_morph_data()

```python
write_morph_data(new_path, curv)
```

### Step 6: Assign curv2 = read_morph_data(...)

```python
curv2 = read_morph_data(new_path)
```

**Verification:**
```python
assert np.array_equal(curv2, curv)
```


## Complete Example

```python
# Workflow
'Test IO of morphometry data file (eg. curvature).'
curv_path = pjoin(data_path, 'surf', 'lh.curv')
curv = read_morph_data(curv_path)
assert -1.0 < curv.min() < 0
assert 0 < curv.max() < 1.0
with InTemporaryDirectory():
    new_path = 'test'
    write_morph_data(new_path, curv)
    curv2 = read_morph_data(new_path)
    assert np.array_equal(curv2, curv)
```

## Next Steps


---

*Source: test_io.py:137 | Complexity: Advanced | Last updated: 2026-05-18*