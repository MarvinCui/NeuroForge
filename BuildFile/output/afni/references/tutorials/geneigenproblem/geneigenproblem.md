# How To: Geneigenproblem

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Solve a generalized eigenvalue problem.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `__future__`
- `_tools`

**Setup Required:**
```python
# Fixtures: dtype, range, func
```

## Step-by-Step Guide

### Step 1: 'Solve a generalized eigenvalue problem.'

```python
'Solve a generalized eigenvalue problem.'
```

**Verification:**
```python
assert z.dtype == dtype
```

### Step 2: Assign dtype = numx.dtype(...)

```python
dtype = numx.dtype(dtype)
```

**Verification:**
```python
assert_array_almost_equal(diag1, w, TESTDECIMALS[dtype])
```

### Step 3: Assign dim = 5

```python
dim = 5
```

**Verification:**
```python
assert_array_almost_equal(diag2, numx.ones(diag2.shape[0]), TESTDECIMALS[dtype])
```

### Step 4: Assign a = utils.symrand(...)

```python
a = utils.symrand(dim, dtype)
```

### Step 5: Assign b = value

```python
b = utils.symrand(dim, dtype) + numx.diag([2.1] * dim).astype(dtype)
```

### Step 6: Assign unknown = func(...)

```python
w, z = func(a, b, range=range)
```

**Verification:**
```python
assert z.dtype == dtype
```

### Step 7: Assign w = w.astype(...)

```python
w = w.astype(dtype)
```

### Step 8: Assign diag1 = value

```python
diag1 = numx.diagonal(utils.mult(utils.hermitian(z), utils.mult(a, z))).real
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(diag1, w, TESTDECIMALS[dtype])
```

### Step 10: Assign diag2 = value

```python
diag2 = numx.diagonal(utils.mult(utils.hermitian(z), utils.mult(b, z))).real
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(diag2, numx.ones(diag2.shape[0]), TESTDECIMALS[dtype])
```

### Step 12: Assign range = value

```python
range = (2, dim - 1)
```

### Step 13: Assign range = None

```python
range = None
```


## Complete Example

```python
# Setup
# Fixtures: dtype, range, func

# Workflow
'Solve a generalized eigenvalue problem.'
dtype = numx.dtype(dtype)
dim = 5
if range:
    range = (2, dim - 1)
else:
    range = None
a = utils.symrand(dim, dtype)
b = utils.symrand(dim, dtype) + numx.diag([2.1] * dim).astype(dtype)
w, z = func(a, b, range=range)
assert z.dtype == dtype
w = w.astype(dtype)
diag1 = numx.diagonal(utils.mult(utils.hermitian(z), utils.mult(a, z))).real
assert_array_almost_equal(diag1, w, TESTDECIMALS[dtype])
diag2 = numx.diagonal(utils.mult(utils.hermitian(z), utils.mult(b, z))).real
assert_array_almost_equal(diag2, numx.ones(diag2.shape[0]), TESTDECIMALS[dtype])
```

## Next Steps


---

*Source: test_utils_generic.py:27 | Complexity: Advanced | Last updated: 2026-05-18*