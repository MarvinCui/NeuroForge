# How To: Scaling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test scaling

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

### Step 1: Assign hdr = AnalyzeHeader(...)

```python
hdr = AnalyzeHeader()
```

**Verification:**
```python
assert_true(hdr.default_x_flip)
```

### Step 2: Call assert_true()

```python
assert_true(hdr.default_x_flip)
```

**Verification:**
```python
assert_array_almost_equal(data, rdata)
```

### Step 3: Assign shape = value

```python
shape = (1, 2, 3)
```

**Verification:**
```python
assert_raises(HeaderTypeError, hdr.data_to_fileobj, data, BytesIO())
```

### Step 4: Call hdr.set_data_shape()

```python
hdr.set_data_shape(shape)
```

**Verification:**
```python
assert_true(np.allclose(data, rdata))
```

### Step 5: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(np.float32)
```

**Verification:**
```python
assert_false(np.allclose(data_p5, rdata))
```

### Step 6: Assign data = np.ones(...)

```python
data = np.ones(shape, dtype=np.float64)
```

### Step 7: Assign S = BytesIO(...)

```python
S = BytesIO()
```

### Step 8: Call hdr.data_to_fileobj()

```python
hdr.data_to_fileobj(data, S)
```

### Step 9: Assign rdata = hdr.data_from_fileobj(...)

```python
rdata = hdr.data_from_fileobj(S)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(data, rdata)
```

### Step 11: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(np.int32)
```

### Step 12: Call assert_raises()

```python
assert_raises(HeaderTypeError, hdr.data_to_fileobj, data, BytesIO())
```

### Step 13: Call _write_data()

```python
_write_data(hdr, data, S)
```

### Step 14: Assign rdata = hdr.data_from_fileobj(...)

```python
rdata = hdr.data_from_fileobj(S)
```

### Step 15: Call assert_true()

```python
assert_true(np.allclose(data, rdata))
```

### Step 16: Assign data_p5 = value

```python
data_p5 = data + 0.5
```

### Step 17: Call _write_data()

```python
_write_data(hdr, data_p5, S)
```

### Step 18: Assign rdata = hdr.data_from_fileobj(...)

```python
rdata = hdr.data_from_fileobj(S)
```

### Step 19: Call assert_false()

```python
assert_false(np.allclose(data_p5, rdata))
```


## Complete Example

```python
# Workflow
hdr = AnalyzeHeader()
assert_true(hdr.default_x_flip)
shape = (1, 2, 3)
hdr.set_data_shape(shape)
hdr.set_data_dtype(np.float32)
data = np.ones(shape, dtype=np.float64)
S = BytesIO()
hdr.data_to_fileobj(data, S)
rdata = hdr.data_from_fileobj(S)
assert_array_almost_equal(data, rdata)
hdr.set_data_dtype(np.int32)
assert_raises(HeaderTypeError, hdr.data_to_fileobj, data, BytesIO())
_write_data(hdr, data, S)
rdata = hdr.data_from_fileobj(S)
assert_true(np.allclose(data, rdata))
data_p5 = data + 0.5
_write_data(hdr, data_p5, S)
rdata = hdr.data_from_fileobj(S)
assert_false(np.allclose(data_p5, rdata))
```

## Next Steps


---

*Source: test_analyze.py:475 | Complexity: Advanced | Last updated: 2026-05-18*