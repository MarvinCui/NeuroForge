# How To: Proxy Slicing

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test proxy slicing

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: n_dim, offset
```

## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (15, 16, 17)[:n_dim]
```

**Verification:**
```python
assert prox.order == order
```

### Step 2: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(np.prod(shape)).reshape(shape)
```

**Verification:**
```python
assert_array_equal(arr[sliceobj], prox[sliceobj])
```

### Step 3: Assign hdr = Nifti1Header(...)

```python
hdr = Nifti1Header()
```

### Step 4: Call hdr.set_data_offset()

```python
hdr.set_data_offset(offset)
```

### Step 5: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(arr.dtype)
```

### Step 6: Call hdr.set_data_shape()

```python
hdr.set_data_shape(shape)
```

### Step 7: Assign fobj = BytesIO(...)

```python
fobj = BytesIO()
```

### Step 8: Call fobj.write()

```python
fobj.write(b'\x00' * offset)
```

### Step 9: Call fobj.write()

```python
fobj.write(arr.tobytes(order=order))
```

### Step 10: Assign prox = klass(...)

```python
prox = klass(fobj, hdr)
```

**Verification:**
```python
assert prox.order == order
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(arr[sliceobj], prox[sliceobj])
```


## Complete Example

```python
# Setup
# Fixtures: n_dim, offset

# Workflow
shape = (15, 16, 17)[:n_dim]
arr = np.arange(np.prod(shape)).reshape(shape)
hdr = Nifti1Header()
hdr.set_data_offset(offset)
hdr.set_data_dtype(arr.dtype)
hdr.set_data_shape(shape)
for order, klass in (('F', ArrayProxy), ('C', CArrayProxy)):
    fobj = BytesIO()
    fobj.write(b'\x00' * offset)
    fobj.write(arr.tobytes(order=order))
    prox = klass(fobj, hdr)
    assert prox.order == order
    for sliceobj in slicer_samples(shape):
        assert_array_equal(arr[sliceobj], prox[sliceobj])
```

## Next Steps


---

*Source: test_arrayproxy.py:162 | Complexity: Advanced | Last updated: 2026-05-18*