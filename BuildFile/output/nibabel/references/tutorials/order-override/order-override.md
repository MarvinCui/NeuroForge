# How To: Order Override

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test order override

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
# Fixtures: order
```

## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (15, 16, 17)
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

### Step 3: Assign fobj = BytesIO(...)

```python
fobj = BytesIO()
```

### Step 4: Call fobj.write()

```python
fobj.write(arr.tobytes(order=order))
```

### Step 5: Assign prox = klass(...)

```python
prox = klass(fobj, (shape, arr.dtype), order=order)
```

**Verification:**
```python
assert prox.order == order
```

### Step 6: Assign sliceobj = value

```python
sliceobj = (None, slice(None), 1, -1)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(arr[sliceobj], prox[sliceobj])
```


## Complete Example

```python
# Setup
# Fixtures: order

# Workflow
shape = (15, 16, 17)
arr = np.arange(np.prod(shape)).reshape(shape)
fobj = BytesIO()
fobj.write(arr.tobytes(order=order))
for klass in (ArrayProxy, CArrayProxy):
    prox = klass(fobj, (shape, arr.dtype), order=order)
    assert prox.order == order
    sliceobj = (None, slice(None), 1, -1)
    assert_array_equal(arr[sliceobj], prox[sliceobj])
```

## Next Steps


---

*Source: test_arrayproxy.py:197 | Complexity: Intermediate | Last updated: 2026-05-18*