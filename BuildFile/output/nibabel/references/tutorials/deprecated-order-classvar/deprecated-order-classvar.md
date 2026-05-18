# How To: Deprecated Order Classvar

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test deprecated order classvar

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
assert prox.order == 'C'
```

### Step 2: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(np.prod(shape)).reshape(shape)
```

**Verification:**
```python
assert_array_equal(prox[sliceobj], cprox[sliceobj])
```

### Step 3: Assign fobj = BytesIO(...)

```python
fobj = BytesIO()
```

**Verification:**
```python
assert prox.order == 'C'
```

### Step 4: Call fobj.write()

```python
fobj.write(arr.tobytes(order='C'))
```

**Verification:**
```python
assert_array_equal(prox[sliceobj], cprox[sliceobj])
```

### Step 5: Assign sliceobj = value

```python
sliceobj = (None, slice(None), 1, -1)
```

**Verification:**
```python
assert prox.order == 'F'
```

### Step 6: Assign fprox = ArrayProxy(...)

```python
fprox = ArrayProxy(fobj, (shape, arr.dtype), order='F')
```

**Verification:**
```python
assert_array_equal(prox[sliceobj], fprox[sliceobj])
```

### Step 7: Assign cprox = ArrayProxy(...)

```python
cprox = ArrayProxy(fobj, (shape, arr.dtype), order='C')
```

### Step 8: Assign cm = pytest.raises(...)

```python
cm = pytest.raises(ExpiredDeprecationError)
```

### Step 9: Assign cm = pytest.deprecated_call(...)

```python
cm = pytest.deprecated_call()
```

### Step 10: Assign prox = DeprecatedCArrayProxy(...)

```python
prox = DeprecatedCArrayProxy(fobj, (shape, arr.dtype))
```

**Verification:**
```python
assert prox.order == 'C'
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(prox[sliceobj], cprox[sliceobj])
```

### Step 12: Assign prox = DeprecatedCArrayProxy(...)

```python
prox = DeprecatedCArrayProxy(fobj, (shape, arr.dtype), order='C')
```

**Verification:**
```python
assert prox.order == 'C'
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(prox[sliceobj], cprox[sliceobj])
```

### Step 14: Assign prox = DeprecatedCArrayProxy(...)

```python
prox = DeprecatedCArrayProxy(fobj, (shape, arr.dtype), order='F')
```

**Verification:**
```python
assert prox.order == 'F'
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(prox[sliceobj], fprox[sliceobj])
```


## Complete Example

```python
# Workflow
shape = (15, 16, 17)
arr = np.arange(np.prod(shape)).reshape(shape)
fobj = BytesIO()
fobj.write(arr.tobytes(order='C'))
sliceobj = (None, slice(None), 1, -1)
fprox = ArrayProxy(fobj, (shape, arr.dtype), order='F')
cprox = ArrayProxy(fobj, (shape, arr.dtype), order='C')
if Version(__version__) >= Version('7.0.0.dev0'):
    cm = pytest.raises(ExpiredDeprecationError)
else:
    cm = pytest.deprecated_call()
with cm:
    prox = DeprecatedCArrayProxy(fobj, (shape, arr.dtype))
    assert prox.order == 'C'
    assert_array_equal(prox[sliceobj], cprox[sliceobj])
with cm:
    prox = DeprecatedCArrayProxy(fobj, (shape, arr.dtype), order='C')
    assert prox.order == 'C'
    assert_array_equal(prox[sliceobj], cprox[sliceobj])
with cm:
    prox = DeprecatedCArrayProxy(fobj, (shape, arr.dtype), order='F')
    assert prox.order == 'F'
    assert_array_equal(prox[sliceobj], fprox[sliceobj])
```

## Next Steps


---

*Source: test_arrayproxy.py:209 | Complexity: Advanced | Last updated: 2026-05-18*