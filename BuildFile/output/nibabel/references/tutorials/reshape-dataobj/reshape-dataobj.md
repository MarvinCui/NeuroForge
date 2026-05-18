# How To: Reshape Dataobj

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test reshape dataobj

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
shape = (1, 2, 3, 4)
```

**Verification:**
```python
assert_array_equal(prox, arr)
```

### Step 2: Assign hdr = FunkyHeader(...)

```python
hdr = FunkyHeader(shape)
```

**Verification:**
```python
assert_array_equal(reshape_dataobj(prox, (2, 3, 4)), np.reshape(arr, (2, 3, 4)))
```

### Step 3: Assign bio = BytesIO(...)

```python
bio = BytesIO()
```

**Verification:**
```python
assert prox.shape == shape
```

### Step 4: Assign prox = ArrayProxy(...)

```python
prox = ArrayProxy(bio, hdr)
```

**Verification:**
```python
assert arr.shape == shape
```

### Step 5: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(np.prod(shape), dtype=prox.dtype).reshape(shape)
```

**Verification:**
```python
assert_array_equal(reshape_dataobj(arr, (2, 3, 4)), np.reshape(arr, (2, 3, 4)))
```

### Step 6: Call bio.write()

```python
bio.write(b'\x00' * prox.offset + arr.tobytes(order='F'))
```

**Verification:**
```python
assert arr.shape == shape
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(prox, arr)
```

**Verification:**
```python
assert_array_equal(reshape_dataobj(ArrGiver(), (2, 3, 4)), np.reshape(arr, (2, 3, 4)))
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(reshape_dataobj(prox, (2, 3, 4)), np.reshape(arr, (2, 3, 4)))
```

**Verification:**
```python
assert arr.shape == shape
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(reshape_dataobj(arr, (2, 3, 4)), np.reshape(arr, (2, 3, 4)))
```

**Verification:**
```python
assert arr.shape == shape
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(reshape_dataobj(ArrGiver(), (2, 3, 4)), np.reshape(arr, (2, 3, 4)))
```

**Verification:**
```python
assert arr.shape == shape
```


## Complete Example

```python
# Workflow
shape = (1, 2, 3, 4)
hdr = FunkyHeader(shape)
bio = BytesIO()
prox = ArrayProxy(bio, hdr)
arr = np.arange(np.prod(shape), dtype=prox.dtype).reshape(shape)
bio.write(b'\x00' * prox.offset + arr.tobytes(order='F'))
assert_array_equal(prox, arr)
assert_array_equal(reshape_dataobj(prox, (2, 3, 4)), np.reshape(arr, (2, 3, 4)))
assert prox.shape == shape
assert arr.shape == shape
assert_array_equal(reshape_dataobj(arr, (2, 3, 4)), np.reshape(arr, (2, 3, 4)))
assert arr.shape == shape

class ArrGiver:

    def __array__(self):
        return arr
assert_array_equal(reshape_dataobj(ArrGiver(), (2, 3, 4)), np.reshape(arr, (2, 3, 4)))
assert arr.shape == shape
```

## Next Steps


---

*Source: test_arrayproxy.py:257 | Complexity: Advanced | Last updated: 2026-05-18*