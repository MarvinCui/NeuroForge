# How To: A2F Order

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test a2f order

## Prerequisites

**Required Modules:**
- `__future__`
- `py3k`
- `tempfile`
- `numpy`
- `tmpdirs`
- `volumeutils`
- `casting`
- `numpy.testing`
- `nose.tools`
- `testing`


## Step-by-Step Guide

### Step 1: Assign ndt = np.dtype(...)

```python
ndt = np.dtype(np.float)
```

**Verification:**
```python
assert_array_equal(data_back, [0.0, 1.0, 2.0])
```

### Step 2: Assign arr = np.array(...)

```python
arr = np.array([0.0, 1.0, 2.0])
```

**Verification:**
```python
assert_array_equal(data_back, arr)
```

### Step 3: Assign str_io = BytesIO(...)

```python
str_io = BytesIO()
```

**Verification:**
```python
assert_array_equal(data_back, arr.T)
```

### Step 4: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, ndt, order='C')
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(data_back, [0.0, 1.0, 2.0])
```

### Step 6: Assign arr = np.array(...)

```python
arr = np.array([[0.0, 1.0], [2.0, 3.0]])
```

### Step 7: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, ndt, order='F')
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(data_back, arr)
```

### Step 9: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, ndt, order='C')
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(data_back, arr.T)
```


## Complete Example

```python
# Workflow
ndt = np.dtype(np.float)
arr = np.array([0.0, 1.0, 2.0])
str_io = BytesIO()
data_back = write_return(arr, str_io, ndt, order='C')
assert_array_equal(data_back, [0.0, 1.0, 2.0])
arr = np.array([[0.0, 1.0], [2.0, 3.0]])
data_back = write_return(arr, str_io, ndt, order='F')
assert_array_equal(data_back, arr)
data_back = write_return(arr, str_io, ndt, order='C')
assert_array_equal(data_back, arr.T)
```

## Next Steps


---

*Source: test_utils.py:179 | Complexity: Advanced | Last updated: 2026-05-18*