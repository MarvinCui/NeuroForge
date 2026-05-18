# How To: A2F Min Max

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test a2f min max

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

### Step 1: Assign str_io = BytesIO(...)

```python
str_io = BytesIO()
```

**Verification:**
```python
assert_array_equal(data_back, [1, 1, 2, 3])
```

### Step 2: Assign arr = np.arange(...)

```python
arr = np.arange(4, dtype=np.float32)
```

**Verification:**
```python
assert_array_equal(data_back, [0, 1, 2, 2])
```

### Step 3: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, np.int, 0, -1, 0.5, 1, 2)
```

**Verification:**
```python
assert_array_equal(data_back, [1, 1, 2, 2])
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(data_back * 0.5 - 1, [1, 1, 2, 2])
```

**Verification:**
```python
assert_array_equal(data_back * 0.5 - 1, [1, 1, 2, 2])
```

### Step 5: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, np.int, 0, 1, -0.5, 1, 2)
```

**Verification:**
```python
assert_array_equal(data_back * -0.5 + 1, [1, 1, 2, 2])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(data_back * -0.5 + 1, [1, 1, 2, 2])
```

### Step 7: Assign arr = np.arange(...)

```python
arr = np.arange(4, dtype=in_dt)
```

### Step 8: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, out_dt, 0, 0, 1, 1)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(data_back, [1, 1, 2, 3])
```

### Step 10: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, out_dt, 0, 0, 1, None, 2)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(data_back, [0, 1, 2, 2])
```

### Step 12: Assign data_back = write_return(...)

```python
data_back = write_return(arr, str_io, out_dt, 0, 0, 1, 1, 2)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(data_back, [1, 1, 2, 2])
```


## Complete Example

```python
# Workflow
str_io = BytesIO()
for in_dt in (np.float32, np.int8):
    for out_dt in (np.float32, np.int8):
        arr = np.arange(4, dtype=in_dt)
        data_back = write_return(arr, str_io, out_dt, 0, 0, 1, 1)
        assert_array_equal(data_back, [1, 1, 2, 3])
        data_back = write_return(arr, str_io, out_dt, 0, 0, 1, None, 2)
        assert_array_equal(data_back, [0, 1, 2, 2])
        data_back = write_return(arr, str_io, out_dt, 0, 0, 1, 1, 2)
        assert_array_equal(data_back, [1, 1, 2, 2])
arr = np.arange(4, dtype=np.float32)
data_back = write_return(arr, str_io, np.int, 0, -1, 0.5, 1, 2)
assert_array_equal(data_back * 0.5 - 1, [1, 1, 2, 2])
data_back = write_return(arr, str_io, np.int, 0, 1, -0.5, 1, 2)
assert_array_equal(data_back * -0.5 + 1, [1, 1, 2, 2])
```

## Next Steps


---

*Source: test_utils.py:156 | Complexity: Advanced | Last updated: 2026-05-18*