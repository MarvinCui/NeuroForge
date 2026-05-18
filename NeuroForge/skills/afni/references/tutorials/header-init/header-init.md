# How To: Header Init

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test header init

## Prerequisites

**Required Modules:**
- `py3k`
- `numpy`
- `spatialimages`
- `unittest`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign hdr = Header(...)

```python
hdr = Header()
```

**Verification:**
```python
assert_equal(hdr.get_data_dtype(), np.dtype(np.float32))
```

### Step 2: Call assert_equal()

```python
assert_equal(hdr.get_data_dtype(), np.dtype(np.float32))
```

**Verification:**
```python
assert_equal(hdr.get_data_shape(), (0,))
```

### Step 3: Call assert_equal()

```python
assert_equal(hdr.get_data_shape(), (0,))
```

**Verification:**
```python
assert_equal(hdr.get_zooms(), (1.0,))
```

### Step 4: Call assert_equal()

```python
assert_equal(hdr.get_zooms(), (1.0,))
```

**Verification:**
```python
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
```

### Step 5: Assign hdr = Header(...)

```python
hdr = Header(np.float64)
```

**Verification:**
```python
assert_equal(hdr.get_data_shape(), (0,))
```

### Step 6: Call assert_equal()

```python
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
```

**Verification:**
```python
assert_equal(hdr.get_zooms(), (1.0,))
```

### Step 7: Call assert_equal()

```python
assert_equal(hdr.get_data_shape(), (0,))
```

**Verification:**
```python
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
```

### Step 8: Call assert_equal()

```python
assert_equal(hdr.get_zooms(), (1.0,))
```

**Verification:**
```python
assert_equal(hdr.get_data_shape(), (1, 2, 3))
```

### Step 9: Assign hdr = Header(...)

```python
hdr = Header(np.float64, shape=(1, 2, 3))
```

**Verification:**
```python
assert_equal(hdr.get_zooms(), (1.0, 1.0, 1.0))
```

### Step 10: Call assert_equal()

```python
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
```

**Verification:**
```python
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
```

### Step 11: Call assert_equal()

```python
assert_equal(hdr.get_data_shape(), (1, 2, 3))
```

**Verification:**
```python
assert_equal(hdr.get_data_shape(), (1, 2, 3))
```

### Step 12: Call assert_equal()

```python
assert_equal(hdr.get_zooms(), (1.0, 1.0, 1.0))
```

**Verification:**
```python
assert_equal(hdr.get_zooms(), (1.0, 1.0, 1.0))
```

### Step 13: Assign hdr = Header(...)

```python
hdr = Header(np.float64, shape=(1, 2, 3), zooms=None)
```

**Verification:**
```python
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
```

### Step 14: Call assert_equal()

```python
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
```

**Verification:**
```python
assert_equal(hdr.get_data_shape(), (1, 2, 3))
```

### Step 15: Call assert_equal()

```python
assert_equal(hdr.get_data_shape(), (1, 2, 3))
```

**Verification:**
```python
assert_equal(hdr.get_zooms(), (3.0, 2.0, 1.0))
```

### Step 16: Call assert_equal()

```python
assert_equal(hdr.get_zooms(), (1.0, 1.0, 1.0))
```

### Step 17: Assign hdr = Header(...)

```python
hdr = Header(np.float64, shape=(1, 2, 3), zooms=(3.0, 2.0, 1.0))
```

### Step 18: Call assert_equal()

```python
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
```

### Step 19: Call assert_equal()

```python
assert_equal(hdr.get_data_shape(), (1, 2, 3))
```

### Step 20: Call assert_equal()

```python
assert_equal(hdr.get_zooms(), (3.0, 2.0, 1.0))
```


## Complete Example

```python
# Workflow
hdr = Header()
assert_equal(hdr.get_data_dtype(), np.dtype(np.float32))
assert_equal(hdr.get_data_shape(), (0,))
assert_equal(hdr.get_zooms(), (1.0,))
hdr = Header(np.float64)
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
assert_equal(hdr.get_data_shape(), (0,))
assert_equal(hdr.get_zooms(), (1.0,))
hdr = Header(np.float64, shape=(1, 2, 3))
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
assert_equal(hdr.get_data_shape(), (1, 2, 3))
assert_equal(hdr.get_zooms(), (1.0, 1.0, 1.0))
hdr = Header(np.float64, shape=(1, 2, 3), zooms=None)
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
assert_equal(hdr.get_data_shape(), (1, 2, 3))
assert_equal(hdr.get_zooms(), (1.0, 1.0, 1.0))
hdr = Header(np.float64, shape=(1, 2, 3), zooms=(3.0, 2.0, 1.0))
assert_equal(hdr.get_data_dtype(), np.dtype(np.float64))
assert_equal(hdr.get_data_shape(), (1, 2, 3))
assert_equal(hdr.get_zooms(), (3.0, 2.0, 1.0))
```

## Next Steps


---

*Source: test_spatialimages.py:27 | Complexity: Advanced | Last updated: 2026-05-18*