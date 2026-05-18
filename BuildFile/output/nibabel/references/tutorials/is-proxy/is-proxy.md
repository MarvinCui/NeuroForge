# How To: Is Proxy

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test is proxy

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

### Step 1: Assign hdr = FunkyHeader(...)

```python
hdr = FunkyHeader((2, 3, 4))
```

**Verification:**
```python
assert is_proxy(prox)
```

### Step 2: Assign bio = BytesIO(...)

```python
bio = BytesIO()
```

**Verification:**
```python
assert not is_proxy(bio)
```

### Step 3: Assign prox = ArrayProxy(...)

```python
prox = ArrayProxy(bio, hdr)
```

**Verification:**
```python
assert not is_proxy(hdr)
```

### Step 4: Assign is_proxy = False

```python
is_proxy = False
```

**Verification:**
```python
assert not is_proxy(np.zeros((2, 3, 4)))
```


## Complete Example

```python
# Workflow
hdr = FunkyHeader((2, 3, 4))
bio = BytesIO()
prox = ArrayProxy(bio, hdr)
assert is_proxy(prox)
assert not is_proxy(bio)
assert not is_proxy(hdr)
assert not is_proxy(np.zeros((2, 3, 4)))

class NP:
    is_proxy = False
assert not is_proxy(NP())
```

## Next Steps


---

*Source: test_arrayproxy.py:241 | Complexity: Intermediate | Last updated: 2026-05-18*