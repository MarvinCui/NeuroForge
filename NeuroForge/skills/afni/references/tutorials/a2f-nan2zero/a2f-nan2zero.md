# How To: A2F Nan2Zero

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test a2f nan2zero

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
assert_array_equal(data_back, arr)
```

### Step 2: Assign str_io = BytesIO(...)

```python
str_io = BytesIO()
```

**Verification:**
```python
assert_array_equal(data_back, arr)
```

### Step 3: Assign arr = np.array(...)

```python
arr = np.array([[np.nan, 0], [0, np.nan]])
```

**Verification:**
```python
assert_array_equal(data_back, [[0, 0], [0, 0]])
```

### Step 4: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, ndt)
```

**Verification:**
```python
assert_array_equal(data_back, arr.astype(np.int64))
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(data_back, arr)
```

### Step 6: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, ndt, nan2zero=True)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(data_back, arr)
```

### Step 8: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, np.dtype(np.int64), nan2zero=True)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(data_back, [[0, 0], [0, 0]])
```

### Step 10: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, np.dtype(np.int64), nan2zero=False)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(data_back, arr.astype(np.int64))
```


## Complete Example

```python
# Workflow
ndt = np.dtype(np.float)
str_io = BytesIO()
arr = np.array([[np.nan, 0], [0, np.nan]])
data_back = write_return(arr, str_io, ndt)
assert_array_equal(data_back, arr)
data_back = write_return(arr, str_io, ndt, nan2zero=True)
assert_array_equal(data_back, arr)
data_back = write_return(arr, str_io, np.dtype(np.int64), nan2zero=True)
assert_array_equal(data_back, [[0, 0], [0, 0]])
data_back = write_return(arr, str_io, np.dtype(np.int64), nan2zero=False)
assert_array_equal(data_back, arr.astype(np.int64))
```

## Next Steps


---

*Source: test_utils.py:194 | Complexity: Advanced | Last updated: 2026-05-18*