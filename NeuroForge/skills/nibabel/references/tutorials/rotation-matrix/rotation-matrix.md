# How To: Rotation Matrix

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test rotation matrix

## Prerequisites

**Required Modules:**
- `gzip`
- `copy`
- `decimal`
- `hashlib`
- `os.path`
- `os.path`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `openers`
- `tests.nibabel_data`
- `volumeutils`


## Step-by-Step Guide

### Step 1: Assign d = value

```python
d = {}
```

**Verification:**
```python
assert_array_equal(dw.rotation_matrix, np.eye(3))
```

### Step 2: Assign unknown = value

```python
d['ImageOrientationPatient'] = [0, 1, 0, 1, 0, 0]
```

**Verification:**
```python
assert_array_equal(dw.rotation_matrix, [[0, 1, 0], [1, 0, 0], [0, 0, -1]])
```

### Step 3: Assign dw = didw.wrapper_from_data(...)

```python
dw = didw.wrapper_from_data(d)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(dw.rotation_matrix, np.eye(3))
```

### Step 5: Assign unknown = value

```python
d['ImageOrientationPatient'] = [1, 0, 0, 0, 1, 0]
```

### Step 6: Assign dw = didw.wrapper_from_data(...)

```python
dw = didw.wrapper_from_data(d)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(dw.rotation_matrix, [[0, 1, 0], [1, 0, 0], [0, 0, -1]])
```


## Complete Example

```python
# Workflow
d = {}
d['ImageOrientationPatient'] = [0, 1, 0, 1, 0, 0]
dw = didw.wrapper_from_data(d)
assert_array_equal(dw.rotation_matrix, np.eye(3))
d['ImageOrientationPatient'] = [1, 0, 0, 0, 1, 0]
dw = didw.wrapper_from_data(d)
assert_array_equal(dw.rotation_matrix, [[0, 1, 0], [1, 0, 0], [0, 0, -1]])
```

## Next Steps


---

*Source: test_dicomwrappers.py:333 | Complexity: Intermediate | Last updated: 2026-05-18*