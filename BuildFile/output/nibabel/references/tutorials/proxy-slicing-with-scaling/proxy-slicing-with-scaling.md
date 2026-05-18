# How To: Proxy Slicing With Scaling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test proxy slicing with scaling

## Prerequisites

**Required Modules:**
- `contextlib`
- `gzip`
- `pickle`
- `io`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `packaging.version`
- `arrayproxy`
- `deprecator`
- `nifti1`
- `openers`
- `testing`
- `tmpdirs`
- `test_fileslice`
- `test_openers`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (15, 16, 17)
```

**Verification:**
```python
assert_array_equal(arr[sliceobj] * 2.0 + 1.0, prox[sliceobj])
```

### Step 2: Assign offset = 20

```python
offset = 20
```

### Step 3: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(np.prod(shape)).reshape(shape)
```

### Step 4: Assign hdr = Nifti1Header(...)

```python
hdr = Nifti1Header()
```

### Step 5: Call hdr.set_data_offset()

```python
hdr.set_data_offset(offset)
```

### Step 6: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(arr.dtype)
```

### Step 7: Call hdr.set_data_shape()

```python
hdr.set_data_shape(shape)
```

### Step 8: Call hdr.set_slope_inter()

```python
hdr.set_slope_inter(2.0, 1.0)
```

### Step 9: Assign fobj = BytesIO(...)

```python
fobj = BytesIO()
```

### Step 10: Call fobj.write()

```python
fobj.write(bytes(offset))
```

### Step 11: Call fobj.write()

```python
fobj.write(arr.tobytes(order='F'))
```

### Step 12: Assign prox = ArrayProxy(...)

```python
prox = ArrayProxy(fobj, hdr)
```

### Step 13: Assign sliceobj = value

```python
sliceobj = (None, slice(None), 1, -1)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(arr[sliceobj] * 2.0 + 1.0, prox[sliceobj])
```


## Complete Example

```python
# Workflow
shape = (15, 16, 17)
offset = 20
arr = np.arange(np.prod(shape)).reshape(shape)
hdr = Nifti1Header()
hdr.set_data_offset(offset)
hdr.set_data_dtype(arr.dtype)
hdr.set_data_shape(shape)
hdr.set_slope_inter(2.0, 1.0)
fobj = BytesIO()
fobj.write(bytes(offset))
fobj.write(arr.tobytes(order='F'))
prox = ArrayProxy(fobj, hdr)
sliceobj = (None, slice(None), 1, -1)
assert_array_equal(arr[sliceobj] * 2.0 + 1.0, prox[sliceobj])
```

## Next Steps


---

*Source: test_arrayproxy.py:179 | Complexity: Advanced | Last updated: 2026-05-18*