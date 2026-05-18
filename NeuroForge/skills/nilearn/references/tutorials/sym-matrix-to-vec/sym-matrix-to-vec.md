# How To: Sym Matrix To Vec

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sym matrix to vec

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign sym = np.ones(...)

```python
sym = np.ones((3, 3))
```

**Verification:**
```python
assert_array_almost_equal(sym_matrix_to_vec(sym), vec)
```

### Step 2: Assign sqrt2 = value

```python
sqrt2 = 1.0 / sqrt(2.0)
```

**Verification:**
```python
assert_array_almost_equal(sym_matrix_to_vec(sym, discard_diagonal=True), vec)
```

### Step 3: Assign vec = np.array(...)

```python
vec = np.array([sqrt2, 1.0, sqrt2, 1.0, 1.0, sqrt2])
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sym_matrix_to_vec(sym), vec)
```

### Step 5: Assign vec = np.array(...)

```python
vec = np.array([1.0, 1.0, 1.0])
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sym_matrix_to_vec(sym, discard_diagonal=True), vec)
```


## Complete Example

```python
# Workflow
sym = np.ones((3, 3))
sqrt2 = 1.0 / sqrt(2.0)
vec = np.array([sqrt2, 1.0, sqrt2, 1.0, 1.0, sqrt2])
assert_array_almost_equal(sym_matrix_to_vec(sym), vec)
vec = np.array([1.0, 1.0, 1.0])
assert_array_almost_equal(sym_matrix_to_vec(sym, discard_diagonal=True), vec)
```

## Next Steps


---

*Source: test_connectivity_matrices.py:518 | Complexity: Intermediate | Last updated: 2026-05-18*