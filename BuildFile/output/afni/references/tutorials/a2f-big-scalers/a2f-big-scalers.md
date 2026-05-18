# How To: A2F Big Scalers

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test a2f big scalers

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

### Step 1: Assign info = type_info(...)

```python
info = type_info(np.float32)
```

**Verification:**
```python
assert_array_equal(data_back, [-128, 0, 127])
```

### Step 2: Assign arr = np.array(...)

```python
arr = np.array([info['min'], np.nan, info['max']], dtype=np.float32)
```

**Verification:**
```python
assert_array_equal(data_back, [-128, 0, 127])
```

### Step 3: Assign str_io = BytesIO(...)

```python
str_io = BytesIO()
```

**Verification:**
```python
assert_array_equal(data_back, [-128, 0, 127])
```

### Step 4: Call array_to_file()

```python
array_to_file(arr, str_io, np.int8, intercept=np.float32(2 ** 120))
```

**Verification:**
```python
assert_array_equal(data_back, [-128, 0, 127])
```

### Step 5: Assign data_back = array_from_file(...)

```python
data_back = array_from_file(arr.shape, np.int8, str_io)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(data_back, [-128, 0, 127])
```

### Step 7: Call str_io.seek()

```python
str_io.seek(0)
```

### Step 8: Call array_to_file()

```python
array_to_file(arr, str_io, np.int8, mn=info['min'], mx=info['max'], intercept=np.float32(2 ** 120))
```

### Step 9: Assign data_back = array_from_file(...)

```python
data_back = array_from_file(arr.shape, np.int8, str_io)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(data_back, [-128, 0, 127])
```

### Step 11: Call str_io.seek()

```python
str_io.seek(0)
```

### Step 12: Call array_to_file()

```python
array_to_file(arr, str_io, np.int8, divslope=np.float32(0.5))
```

### Step 13: Assign data_back = array_from_file(...)

```python
data_back = array_from_file(arr.shape, np.int8, str_io)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(data_back, [-128, 0, 127])
```

### Step 15: Call str_io.seek()

```python
str_io.seek(0)
```

### Step 16: Call array_to_file()

```python
array_to_file(arr, str_io, np.int8, mn=info['min'], mx=info['max'], divslope=np.float32(0.5))
```

### Step 17: Assign data_back = array_from_file(...)

```python
data_back = array_from_file(arr.shape, np.int8, str_io)
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(data_back, [-128, 0, 127])
```


## Complete Example

```python
# Workflow
info = type_info(np.float32)
arr = np.array([info['min'], np.nan, info['max']], dtype=np.float32)
str_io = BytesIO()
array_to_file(arr, str_io, np.int8, intercept=np.float32(2 ** 120))
data_back = array_from_file(arr.shape, np.int8, str_io)
assert_array_equal(data_back, [-128, 0, 127])
str_io.seek(0)
array_to_file(arr, str_io, np.int8, mn=info['min'], mx=info['max'], intercept=np.float32(2 ** 120))
data_back = array_from_file(arr.shape, np.int8, str_io)
assert_array_equal(data_back, [-128, 0, 127])
str_io.seek(0)
array_to_file(arr, str_io, np.int8, divslope=np.float32(0.5))
data_back = array_from_file(arr.shape, np.int8, str_io)
assert_array_equal(data_back, [-128, 0, 127])
str_io.seek(0)
array_to_file(arr, str_io, np.int8, mn=info['min'], mx=info['max'], divslope=np.float32(0.5))
data_back = array_from_file(arr.shape, np.int8, str_io)
assert_array_equal(data_back, [-128, 0, 127])
```

## Next Steps


---

*Source: test_utils.py:257 | Complexity: Advanced | Last updated: 2026-05-18*