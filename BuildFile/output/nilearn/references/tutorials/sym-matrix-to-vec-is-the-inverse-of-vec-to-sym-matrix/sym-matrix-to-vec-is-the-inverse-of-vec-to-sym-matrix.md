# How To: Sym Matrix To Vec Is The Inverse Of Vec To Sym Matrix

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sym matrix to vec is the inverse of vec to sym matrix

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `warnings`
- `math`
- `numpy`
- `pytest`
- `numpy.testing`
- `pandas`
- `scipy`
- `sklearn.covariance`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.extmath`
- `nilearn._utils.versions`
- `nilearn.connectome.connectivity_matrices`
- `nilearn.tests.test_signal`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign n = 5

```python
n = 5
```

**Verification:**
```python
assert_array_almost_equal(sym_matrix_to_vec(sym), vec)
```

### Step 2: Assign p = value

```python
p = n * (n + 1) // 2
```

**Verification:**
```python
assert_array_almost_equal(sym_matrix_to_vec(sym, discard_diagonal=True), vec)
```

### Step 3: Assign vec = rng.random(...)

```python
vec = rng.random(p)
```

**Verification:**
```python
assert_array_almost_equal(sym_matrix_to_vec(syms), vecs)
```

### Step 4: Assign sym = vec_to_sym_matrix(...)

```python
sym = vec_to_sym_matrix(vec)
```

**Verification:**
```python
assert_array_almost_equal(sym_matrix_to_vec(syms, discard_diagonal=True), vecs)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sym_matrix_to_vec(sym), vec)
```

### Step 6: Assign diagonal = rng.random(...)

```python
diagonal = rng.random(n + 1)
```

### Step 7: Assign sym = vec_to_sym_matrix(...)

```python
sym = vec_to_sym_matrix(vec, diagonal=diagonal)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sym_matrix_to_vec(sym, discard_diagonal=True), vec)
```

### Step 9: Assign vecs = np.asarray(...)

```python
vecs = np.asarray([vec, 2.0 * vec, 0.5 * vec])
```

### Step 10: Assign syms = vec_to_sym_matrix(...)

```python
syms = vec_to_sym_matrix(vecs)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sym_matrix_to_vec(syms), vecs)
```

### Step 12: Assign diagonals = np.asarray(...)

```python
diagonals = np.asarray([diagonal, 3.0 * diagonal, -diagonal])
```

### Step 13: Assign syms = vec_to_sym_matrix(...)

```python
syms = vec_to_sym_matrix(vecs, diagonal=diagonals)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sym_matrix_to_vec(syms, discard_diagonal=True), vecs)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
n = 5
p = n * (n + 1) // 2
vec = rng.random(p)
sym = vec_to_sym_matrix(vec)
assert_array_almost_equal(sym_matrix_to_vec(sym), vec)
diagonal = rng.random(n + 1)
sym = vec_to_sym_matrix(vec, diagonal=diagonal)
assert_array_almost_equal(sym_matrix_to_vec(sym, discard_diagonal=True), vec)
vecs = np.asarray([vec, 2.0 * vec, 0.5 * vec])
syms = vec_to_sym_matrix(vecs)
assert_array_almost_equal(sym_matrix_to_vec(syms), vecs)
diagonals = np.asarray([diagonal, 3.0 * diagonal, -diagonal])
syms = vec_to_sym_matrix(vecs, diagonal=diagonals)
assert_array_almost_equal(sym_matrix_to_vec(syms, discard_diagonal=True), vecs)
```

## Next Steps


---

*Source: test_connectivity_matrices.py:532 | Complexity: Advanced | Last updated: 2026-05-18*