# How To: Shapes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test shapes

## Prerequisites

**Required Modules:**
- `os`
- `re`
- `logging`
- `pickle`
- `numpy`
- `py3k`
- `volumeutils`
- `spatialimages`
- `analyze`
- `nifti1`
- `loadsave`
- `casting`
- `numpy.testing`
- `testing`
- `test_wrapstruct`


## Step-by-Step Guide

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert_equal(hdr.get_data_shape(), shape)
```

### Step 2: Assign dim_dtype = value

```python
dim_dtype = hdr.structarr['dim'].dtype
```

**Verification:**
```python
assert_equal(hdr.get_data_shape(), shape)
```

### Step 3: Assign mx = as_int(...)

```python
mx = as_int(np.iinfo(dim_dtype).max)
```

**Verification:**
```python
assert_raises(HeaderDataError, hdr.set_data_shape, shape)
```

### Step 4: Assign shape = value

```python
shape = (mx,)
```

**Verification:**
```python
assert_equal(hdr.get_data_shape(), shape)
```

### Step 5: Call hdr.set_data_shape()

```python
hdr.set_data_shape(shape)
```

### Step 6: Call assert_equal()

```python
assert_equal(hdr.get_data_shape(), shape)
```

### Step 7: Assign shape = value

```python
shape = (mx + 1,)
```

### Step 8: Call assert_raises()

```python
assert_raises(HeaderDataError, hdr.set_data_shape, shape)
```

### Step 9: Assign shape = value

```python
shape = (2, 3, 4)
```

### Step 10: Call hdr.set_data_shape()

```python
hdr.set_data_shape(shape)
```

### Step 11: Call assert_equal()

```python
assert_equal(hdr.get_data_shape(), shape)
```

### Step 12: Call hdr.set_data_shape()

```python
hdr.set_data_shape(constructor(shape))
```

### Step 13: Call assert_equal()

```python
assert_equal(hdr.get_data_shape(), shape)
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
for shape in ((2, 3, 4), (2, 3, 4, 5), (2, 3), (2,)):
    hdr.set_data_shape(shape)
    assert_equal(hdr.get_data_shape(), shape)
dim_dtype = hdr.structarr['dim'].dtype
mx = as_int(np.iinfo(dim_dtype).max)
shape = (mx,)
hdr.set_data_shape(shape)
assert_equal(hdr.get_data_shape(), shape)
shape = (mx + 1,)
assert_raises(HeaderDataError, hdr.set_data_shape, shape)
shape = (2, 3, 4)
for constructor in (list, tuple, np.array):
    hdr.set_data_shape(constructor(shape))
    assert_equal(hdr.get_data_shape(), shape)
```

## Next Steps


---

*Source: test_analyze.py:222 | Complexity: Advanced | Last updated: 2026-05-18*