# How To: Reshaped Is Proxy

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test reshaped is proxy

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
assert isinstance(prox.reshape((2, 3, 4)), ArrayProxy)
```

### Step 2: Assign hdr = FunkyHeader(...)

```python
hdr = FunkyHeader(shape)
```

**Verification:**
```python
assert isinstance(minus1, ArrayProxy)
```

### Step 3: Assign bio = BytesIO(...)

```python
bio = BytesIO()
```

**Verification:**
```python
assert minus1.shape == (2, 3, 4)
```

### Step 4: Assign prox = ArrayProxy(...)

```python
prox = ArrayProxy(bio, hdr)
```

**Verification:**
```python
assert isinstance(prox.reshape((2, 3, 4)), ArrayProxy)
```

### Step 5: Assign minus1 = prox.reshape(...)

```python
minus1 = prox.reshape((2, -1, 4))
```

**Verification:**
```python
assert isinstance(minus1, ArrayProxy)
```

### Step 6: Call prox.reshape()

```python
prox.reshape((-1, -1, 4))
```

### Step 7: Call prox.reshape()

```python
prox.reshape((2, 3, 5))
```

### Step 8: Call prox.reshape()

```python
prox.reshape((2, -1, 5))
```


## Complete Example

```python
# Workflow
shape = (1, 2, 3, 4)
hdr = FunkyHeader(shape)
bio = BytesIO()
prox = ArrayProxy(bio, hdr)
assert isinstance(prox.reshape((2, 3, 4)), ArrayProxy)
minus1 = prox.reshape((2, -1, 4))
assert isinstance(minus1, ArrayProxy)
assert minus1.shape == (2, 3, 4)
with pytest.raises(ValueError):
    prox.reshape((-1, -1, 4))
with pytest.raises(ValueError):
    prox.reshape((2, 3, 5))
with pytest.raises(ValueError):
    prox.reshape((2, -1, 5))
```

## Next Steps


---

*Source: test_arrayproxy.py:280 | Complexity: Advanced | Last updated: 2026-05-18*