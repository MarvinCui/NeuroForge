# How To: Array To File

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test array to file

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

### Step 1: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(10).reshape(5, 2)
```

**Verification:**
```python
assert_array_almost_equal(arr, data_back)
```

### Step 2: Assign str_io = BytesIO(...)

```python
str_io = BytesIO()
```

### Step 3: Assign dt = np.dtype(...)

```python
dt = np.dtype(tp)
```

### Step 4: Assign ndt = dt.newbyteorder(...)

```python
ndt = dt.newbyteorder(code)
```

### Step 5: Assign unknown = calculate_scale(...)

```python
scale, intercept, mn, mx = calculate_scale(arr, ndt, allow_intercept)
```

### Step 6: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, ndt, 0, intercept, scale)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(arr, data_back)
```


## Complete Example

```python
# Workflow
arr = np.arange(10).reshape(5, 2)
str_io = BytesIO()
for tp in (np.uint64, np.float, np.complex):
    dt = np.dtype(tp)
    for code in '<>':
        ndt = dt.newbyteorder(code)
        for allow_intercept in (True, False):
            scale, intercept, mn, mx = calculate_scale(arr, ndt, allow_intercept)
            data_back = write_return(arr, str_io, ndt, 0, intercept, scale)
            assert_array_almost_equal(arr, data_back)
```

## Next Steps


---

*Source: test_utils.py:109 | Complexity: Intermediate | Last updated: 2026-05-18*