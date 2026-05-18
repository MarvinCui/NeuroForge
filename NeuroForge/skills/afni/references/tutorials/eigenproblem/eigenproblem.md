# How To: Eigenproblem

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Solve a standard eigenvalue problem.

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

### Step 1: 'Solve a standard eigenvalue problem.'

```python
'Solve a standard eigenvalue problem.'
```

**Verification:**
```python
assert_type_equal(z.dtype, dtype)
```

### Step 2: Assign dtype = numx.dtype(...)

```python
dtype = numx.dtype(dtype)
```

**Verification:**
```python
assert_array_almost_equal(diag, w, TESTDECIMALS[dtype])
```

### Step 3: Assign dim = 5

```python
dim = 5
```

### Step 4: Assign a = value

```python
a = utils.symrand(dim, dtype) + numx.diag([2.1] * dim).astype(dtype)
```

### Step 5: Assign unknown = func(...)

```python
w, z = func(a, range=range)
```

### Step 6: Call assert_type_equal()

```python
assert_type_equal(z.dtype, dtype)
```

### Step 7: Assign w = w.astype(...)

```python
w = w.astype(dtype)
```

### Step 8: Assign diag = value

```python
diag = numx.diagonal(utils.mult(utils.hermitian(z), utils.mult(a, z))).real
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(diag, w, TESTDECIMALS[dtype])
```

### Step 10: Assign range = value

```python
range = (2, dim - 1)
```

### Step 11: Assign range = None

```python
range = None
```


## Complete Example

```python
# Setup
# Fixtures: dtype, range, func

# Workflow
'Solve a standard eigenvalue problem.'
dtype = numx.dtype(dtype)
dim = 5
if range:
    range = (2, dim - 1)
else:
    range = None
a = utils.symrand(dim, dtype) + numx.diag([2.1] * dim).astype(dtype)
w, z = func(a, range=range)
assert_type_equal(z.dtype, dtype)
w = w.astype(dtype)
diag = numx.diagonal(utils.mult(utils.hermitian(z), utils.mult(a, z))).real
assert_array_almost_equal(diag, w, TESTDECIMALS[dtype])
```

## Next Steps


---

*Source: test_utils_generic.py:10 | Complexity: Advanced | Last updated: 2026-05-18*