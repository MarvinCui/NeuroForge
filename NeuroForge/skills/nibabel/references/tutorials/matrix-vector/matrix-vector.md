# How To: Matrix Vector

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test matrix vector

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `pytest`
- `numpy.testing`
- `affines`
- `eulerangles`
- `orientations`
- `math`


## Step-by-Step Guide

### Step 1: Assign unknown = to_matvec(...)

```python
newmat, newvec = to_matvec(xform.tolist())
```

**Verification:**
```python
assert_array_equal(newmat, mat)
```

### Step 2: Call assert_array_equal()

```python
assert_array_equal(newmat, mat)
```

**Verification:**
```python
assert_array_equal(newvec, vec)
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(newvec, vec)
```

**Verification:**
```python
assert newvec.shape == (M - 1,)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(from_matvec(mat.tolist(), vec.tolist()), xform)
```

**Verification:**
```python
assert_array_equal(from_matvec(mat, vec), xform)
```

### Step 5: Assign xform = np.zeros(...)

```python
xform = np.zeros((M, N))
```

**Verification:**
```python
assert_array_equal(from_matvec(mat), xform)
```

### Step 6: Assign unknown = np.random.normal(...)

```python
xform[:-1, :] = np.random.normal(size=(M - 1, N))
```

**Verification:**
```python
assert_array_equal(from_matvec(mat, None), xform)
```

### Step 7: Assign unknown = 1

```python
xform[-1, -1] = 1
```

**Verification:**
```python
assert_array_equal(newmat, mat)
```

### Step 8: Assign unknown = to_matvec(...)

```python
newmat, newvec = to_matvec(xform)
```

**Verification:**
```python
assert_array_equal(newvec, vec)
```

### Step 9: Assign mat = value

```python
mat = xform[:-1, :-1]
```

**Verification:**
```python
assert_array_equal(from_matvec(mat.tolist(), vec.tolist()), xform)
```

### Step 10: Assign vec = value

```python
vec = xform[:-1, -1]
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(newmat, mat)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(newvec, vec)
```

**Verification:**
```python
assert newvec.shape == (M - 1,)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(from_matvec(mat, vec), xform)
```

### Step 14: Assign xform_not = value

```python
xform_not = xform[:]
```

### Step 15: Assign unknown = 0

```python
xform_not[:-1, :] = 0
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(from_matvec(mat), xform)
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(from_matvec(mat, None), xform)
```


## Complete Example

```python
# Workflow
for M, N in ((4, 4), (5, 4), (4, 5)):
    xform = np.zeros((M, N))
    xform[:-1, :] = np.random.normal(size=(M - 1, N))
    xform[-1, -1] = 1
    newmat, newvec = to_matvec(xform)
    mat = xform[:-1, :-1]
    vec = xform[:-1, -1]
    assert_array_equal(newmat, mat)
    assert_array_equal(newvec, vec)
    assert newvec.shape == (M - 1,)
    assert_array_equal(from_matvec(mat, vec), xform)
    xform_not = xform[:]
    xform_not[:-1, :] = 0
    assert_array_equal(from_matvec(mat), xform)
    assert_array_equal(from_matvec(mat, None), xform)
newmat, newvec = to_matvec(xform.tolist())
assert_array_equal(newmat, mat)
assert_array_equal(newvec, vec)
assert_array_equal(from_matvec(mat.tolist(), vec.tolist()), xform)
```

## Next Steps


---

*Source: test_affines.py:84 | Complexity: Advanced | Last updated: 2026-05-18*