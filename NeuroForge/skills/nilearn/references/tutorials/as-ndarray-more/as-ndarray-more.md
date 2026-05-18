# How To: As Ndarray More

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test as ndarray more

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `nilearn._utils.numpy_conversions`


## Step-by-Step Guide

### Step 1: Assign arr1 = value

```python
arr1 = [0, 1, 2, 3]
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 2: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1)
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 3: Assign arr1 = value

```python
arr1 = [0, 1, 2, 3]
```

**Verification:**
```python
assert arr2.dtype == float
```

### Step 4: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1, copy=True)
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 5: Assign arr1 = value

```python
arr1 = [0, 1, 2, 3]
```

**Verification:**
```python
assert arr2.dtype == float
```

### Step 6: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1, dtype=float)
```

**Verification:**
```python
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
```

### Step 7: Assign arr1 = value

```python
arr1 = [[0, 1, 2, 3], [0, 1, 2, 3]]
```

**Verification:**
```python
assert not are_arrays_identical(arr1[0], arr2[0])
```

### Step 8: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1, dtype=float, order='F')
```

**Verification:**
```python
assert arr2.dtype == float
```

### Step 9: Call as_ndarray()

```python
as_ndarray('test_string')
```

### Step 10: Call as_ndarray()

```python
as_ndarray([], order='invalid')
```


## Complete Example

```python
# Workflow
arr1 = [0, 1, 2, 3]
arr2 = as_ndarray(arr1)
assert not are_arrays_identical(arr1, arr2)
arr1 = [0, 1, 2, 3]
arr2 = as_ndarray(arr1, copy=True)
assert not are_arrays_identical(arr1, arr2)
arr1 = [0, 1, 2, 3]
arr2 = as_ndarray(arr1, dtype=float)
assert arr2.dtype == float
assert not are_arrays_identical(arr1, arr2)
arr1 = [[0, 1, 2, 3], [0, 1, 2, 3]]
arr2 = as_ndarray(arr1, dtype=float, order='F')
assert arr2.dtype == float
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
assert not are_arrays_identical(arr1[0], arr2[0])
with pytest.raises(TypeError):
    as_ndarray('test_string')
with pytest.raises(ValueError):
    as_ndarray([], order='invalid')
```

## Next Steps


---

*Source: test_numpy_conversions.py:202 | Complexity: Advanced | Last updated: 2026-05-18*