# How To: Tuplespec

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test tuplespec

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

### Step 1: Assign bio = BytesIO(...)

```python
bio = BytesIO()
```

**Verification:**
```python
assert getattr(ap_header, prop) == getattr(ap_tuple, prop)
```

### Step 2: Assign shape = value

```python
shape = [2, 3, 4]
```

**Verification:**
```python
assert_array_equal(getattr(ap_header, method)(*args), getattr(ap_tuple, method)(*args))
```

### Step 3: Assign dtype = value

```python
dtype = np.int32
```

### Step 4: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(24, dtype=dtype).reshape(shape)
```

### Step 5: Call bio.seek()

```python
bio.seek(16)
```

### Step 6: Call bio.write()

```python
bio.write(arr.tobytes(order='F'))
```

### Step 7: Assign hdr = FunkyHeader(...)

```python
hdr = FunkyHeader(shape)
```

### Step 8: Assign tuple_spec = value

```python
tuple_spec = (hdr.get_data_shape(), hdr.get_data_dtype(), hdr.get_data_offset(), 1.0, 0.0)
```

### Step 9: Assign ap_header = ArrayProxy(...)

```python
ap_header = ArrayProxy(bio, hdr)
```

### Step 10: Assign ap_tuple = ArrayProxy(...)

```python
ap_tuple = ArrayProxy(bio, tuple_spec)
```

**Verification:**
```python
assert getattr(ap_header, prop) == getattr(ap_tuple, prop)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(getattr(ap_header, method)(*args), getattr(ap_tuple, method)(*args))
```

### Step 12: Call ArrayProxy()

```python
ArrayProxy(bio, tuple_spec[:n])
```

### Step 13: Call ArrayProxy()

```python
ArrayProxy(bio, ())
```

### Step 14: Call ArrayProxy()

```python
ArrayProxy(bio, tuple_spec[:1])
```

### Step 15: Call ArrayProxy()

```python
ArrayProxy(bio, tuple_spec + ('error',))
```


## Complete Example

```python
# Workflow
bio = BytesIO()
shape = [2, 3, 4]
dtype = np.int32
arr = np.arange(24, dtype=dtype).reshape(shape)
bio.seek(16)
bio.write(arr.tobytes(order='F'))
hdr = FunkyHeader(shape)
tuple_spec = (hdr.get_data_shape(), hdr.get_data_dtype(), hdr.get_data_offset(), 1.0, 0.0)
ap_header = ArrayProxy(bio, hdr)
ap_tuple = ArrayProxy(bio, tuple_spec)
for prop in ('shape', 'dtype', 'offset', 'slope', 'inter', 'is_proxy'):
    assert getattr(ap_header, prop) == getattr(ap_tuple, prop)
for method, args in (('get_unscaled', ()), ('__array__', ()), ('__getitem__', ((0, 2, 1),))):
    assert_array_equal(getattr(ap_header, method)(*args), getattr(ap_tuple, method)(*args))
for n in range(2, 5):
    ArrayProxy(bio, tuple_spec[:n])
with pytest.raises(TypeError):
    ArrayProxy(bio, ())
with pytest.raises(TypeError):
    ArrayProxy(bio, tuple_spec[:1])
with pytest.raises(TypeError):
    ArrayProxy(bio, tuple_spec + ('error',))
```

## Next Steps


---

*Source: test_arrayproxy.py:101 | Complexity: Advanced | Last updated: 2026-05-18*