# How To: Orthogonal

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test orthogonal

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

### Step 1: Assign dw = didw.wrapper_from_file(...)

```python
dw = didw.wrapper_from_file(DATA_FILE_SLC_NORM)
```

**Verification:**
```python
assert np.allclose(np.eye(3), np.dot(R, R.T), atol=1e-06)
```

### Step 2: Assign R = value

```python
R = dw.rotation_matrix
```

**Verification:**
```python
assert_array_equal(dw.rotation_matrix, np.eye(3))
```

### Step 3: Assign d = value

```python
d = {}
```

**Verification:**
```python
assert_array_almost_equal(dw.rotation_matrix, np.eye(3), 5)
```

### Step 4: Assign unknown = value

```python
d['ImageOrientationPatient'] = [0, 1, 0, 1, 0, 0]
```

### Step 5: Assign dw = didw.wrapper_from_data(...)

```python
dw = didw.wrapper_from_data(d)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(dw.rotation_matrix, np.eye(3))
```

### Step 7: Assign unknown = value

```python
d['ImageOrientationPatient'] = [1e-05, 1, 0, 1, 0, 0]
```

### Step 8: Assign dw = didw.wrapper_from_data(...)

```python
dw = didw.wrapper_from_data(d)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(dw.rotation_matrix, np.eye(3), 5)
```

### Step 10: Assign unknown = value

```python
d['ImageOrientationPatient'] = [0.0001, 1, 0, 1, 0, 0]
```

### Step 11: Assign dw = didw.wrapper_from_data(...)

```python
dw = didw.wrapper_from_data(d)
```

### Step 12: dw.rotation_matrix

```python
dw.rotation_matrix
```


## Complete Example

```python
# Workflow
dw = didw.wrapper_from_file(DATA_FILE_SLC_NORM)
R = dw.rotation_matrix
assert np.allclose(np.eye(3), np.dot(R, R.T), atol=1e-06)
d = {}
d['ImageOrientationPatient'] = [0, 1, 0, 1, 0, 0]
dw = didw.wrapper_from_data(d)
assert_array_equal(dw.rotation_matrix, np.eye(3))
d['ImageOrientationPatient'] = [1e-05, 1, 0, 1, 0, 0]
dw = didw.wrapper_from_data(d)
assert_array_almost_equal(dw.rotation_matrix, np.eye(3), 5)
d['ImageOrientationPatient'] = [0.0001, 1, 0, 1, 0, 0]
dw = didw.wrapper_from_data(d)
with pytest.raises(didw.WrapperPrecisionError):
    dw.rotation_matrix
```

## Next Steps


---

*Source: test_dicomwrappers.py:312 | Complexity: Advanced | Last updated: 2026-05-18*