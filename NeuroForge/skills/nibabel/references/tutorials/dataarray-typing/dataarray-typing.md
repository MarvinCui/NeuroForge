# How To: Dataarray Typing

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test dataarray typing

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: label
```

## Step-by-Step Guide

### Step 1: Assign dtype = value

```python
dtype = data_type_codes.dtype[label]
```

**Verification:**
```python
assert GiftiDataArray(arr).datatype == code
```

### Step 2: Assign code = value

```python
code = data_type_codes.code[label]
```

**Verification:**
```python
assert GiftiDataArray(arr, datatype=label).datatype == code
```

### Step 3: Assign arr = np.zeros(...)

```python
arr = np.zeros((5,), dtype=dtype)
```

**Verification:**
```python
assert GiftiDataArray(arr, datatype=code).datatype == code
```

### Step 4: Assign gda = GiftiDataArray(...)

```python
gda = GiftiDataArray()
```

**Verification:**
```python
assert GiftiDataArray(arr, datatype=dtype).datatype == code
```

### Step 5: Assign gda.data = arr

```python
gda.data = arr
```

**Verification:**
```python
assert gda.data.dtype == dtype
```

### Step 6: Assign gda.datatype = value

```python
gda.datatype = data_type_codes.code[label]
```

**Verification:**
```python
assert gda.datatype == data_type_codes.code[label]
```

### Step 7: Call GiftiDataArray()

```python
GiftiDataArray(arr)
```


## Complete Example

```python
# Setup
# Fixtures: label

# Workflow
dtype = data_type_codes.dtype[label]
code = data_type_codes.code[label]
arr = np.zeros((5,), dtype=dtype)
if dtype in ('uint8', 'int32', 'float32'):
    assert GiftiDataArray(arr).datatype == code
else:
    with pytest.raises(ValueError):
        GiftiDataArray(arr)
assert GiftiDataArray(arr, datatype=label).datatype == code
assert GiftiDataArray(arr, datatype=code).datatype == code
if dtype != np.dtype('void'):
    assert GiftiDataArray(arr, datatype=dtype).datatype == code
gda = GiftiDataArray()
gda.data = arr
gda.datatype = data_type_codes.code[label]
assert gda.data.dtype == dtype
assert gda.datatype == data_type_codes.code[label]
```

## Next Steps


---

*Source: test_gifti.py:236 | Complexity: Intermediate | Last updated: 2026-05-18*