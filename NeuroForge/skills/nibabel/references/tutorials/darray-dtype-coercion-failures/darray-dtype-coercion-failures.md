# How To: Darray Dtype Coercion Failures

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test darray dtype coercion failures

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel.tmpdirs`
- `fileholders`
- `nifti1`
- `testing`
- `test_parse_gifti_fast`
- `gifti`


## Step-by-Step Guide

### Step 1: Assign dtypes = value

```python
dtypes = (np.uint8, np.int32, np.int64, np.float32, np.float64)
```

**Verification:**
```python
assert np.dtype(da_copy.data.dtype) == np.dtype(darray_dtype)
```

### Step 2: Assign encodings = value

```python
encodings = ('ASCII', 'B64BIN', 'B64GZ')
```

**Verification:**
```python
assert_array_equal(da_copy.data, da.data)
```

### Step 3: Assign da = GiftiDataArray(...)

```python
da = GiftiDataArray(np.arange(10, dtype=data_dtype), encoding=encoding, intent='NIFTI_INTENT_NODE_INDEX', datatype=darray_dtype)
```

### Step 4: Assign gii = GiftiImage(...)

```python
gii = GiftiImage(darrays=[da])
```

### Step 5: Assign gii_copy = GiftiImage.from_bytes(...)

```python
gii_copy = GiftiImage.from_bytes(gii.to_bytes(mode='force'))
```

### Step 6: Assign da_copy = value

```python
da_copy = gii_copy.darrays[0]
```

**Verification:**
```python
assert np.dtype(da_copy.data.dtype) == np.dtype(darray_dtype)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(da_copy.data, da.data)
```


## Complete Example

```python
# Workflow
dtypes = (np.uint8, np.int32, np.int64, np.float32, np.float64)
encodings = ('ASCII', 'B64BIN', 'B64GZ')
for data_dtype, darray_dtype, encoding in itertools.product(dtypes, dtypes, encodings):
    da = GiftiDataArray(np.arange(10, dtype=data_dtype), encoding=encoding, intent='NIFTI_INTENT_NODE_INDEX', datatype=darray_dtype)
    gii = GiftiImage(darrays=[da])
    gii_copy = GiftiImage.from_bytes(gii.to_bytes(mode='force'))
    da_copy = gii_copy.darrays[0]
    assert np.dtype(da_copy.data.dtype) == np.dtype(darray_dtype)
    assert_array_equal(da_copy.data, da.data)
```

## Next Steps


---

*Source: test_gifti.py:548 | Complexity: Intermediate | Last updated: 2026-05-18*