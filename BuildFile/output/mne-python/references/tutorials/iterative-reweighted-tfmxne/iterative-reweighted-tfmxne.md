# How To: Iterative Reweighted Tfmxne

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test convergence of irTF-MxNE solver.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.inverse_sparse.mxne_optim`
- `mne.time_frequency._stft`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test convergence of irTF-MxNE solver.'

```python
'Test convergence of irTF-MxNE solver.'
```

**Verification:**
```python
assert_allclose(X_hat_tf, X_hat_bcd, rtol=0.001)
```

### Step 2: Assign unknown = _generate_tf_data(...)

```python
M, G, true_active_set = _generate_tf_data()
```

**Verification:**
```python
assert_array_equal(np.where(active_set)[0], true_active_set)
```

### Step 3: Assign alpha_space = 38.0

```python
alpha_space = 38.0
```

**Verification:**
```python
assert_array_equal(np.where(active_set)[0], [0, 1, 2, 3, 4])
```

### Step 4: Assign alpha_time = 0.5

```python
alpha_time = 0.5
```

**Verification:**
```python
assert_array_equal(np.where(active_set)[0], [0, 1, 4, 5])
```

### Step 5: Assign unknown = value

```python
tstep, wsize = ([4, 2], [64, 16])
```

### Step 6: Assign unknown = tf_mixed_norm_solver(...)

```python
X_hat_tf, _, _ = tf_mixed_norm_solver(M, G, alpha_space, alpha_time, maxit=1000, tol=0.0001, wsize=wsize, tstep=tstep, verbose=False, n_orient=1, debias=False)
```

### Step 7: Assign unknown = iterative_tf_mixed_norm_solver(...)

```python
X_hat_bcd, active_set, _ = iterative_tf_mixed_norm_solver(M, G, alpha_space, alpha_time, 1, wsize=wsize, tstep=tstep, maxit=1000, tol=0.0001, debias=False, verbose=False)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(X_hat_tf, X_hat_bcd, rtol=0.001)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(np.where(active_set)[0], true_active_set)
```

### Step 10: Assign alpha_space = 50.0

```python
alpha_space = 50.0
```

### Step 11: Assign unknown = iterative_tf_mixed_norm_solver(...)

```python
X_hat_bcd, active_set, _ = iterative_tf_mixed_norm_solver(M, G, alpha_space, alpha_time, 3, wsize=wsize, tstep=tstep, n_orient=5, maxit=1000, tol=0.0001, debias=False, verbose=False)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(np.where(active_set)[0], [0, 1, 2, 3, 4])
```

### Step 13: Assign alpha_space = 40.0

```python
alpha_space = 40.0
```

### Step 14: Assign unknown = iterative_tf_mixed_norm_solver(...)

```python
X_hat_bcd, active_set, _ = iterative_tf_mixed_norm_solver(M, G, alpha_space, alpha_time, 2, wsize=wsize, tstep=tstep, n_orient=2, maxit=1000, tol=0.0001, debias=False, verbose=False)
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(np.where(active_set)[0], [0, 1, 4, 5])
```


## Complete Example

```python
# Workflow
'Test convergence of irTF-MxNE solver.'
M, G, true_active_set = _generate_tf_data()
alpha_space = 38.0
alpha_time = 0.5
tstep, wsize = ([4, 2], [64, 16])
X_hat_tf, _, _ = tf_mixed_norm_solver(M, G, alpha_space, alpha_time, maxit=1000, tol=0.0001, wsize=wsize, tstep=tstep, verbose=False, n_orient=1, debias=False)
X_hat_bcd, active_set, _ = iterative_tf_mixed_norm_solver(M, G, alpha_space, alpha_time, 1, wsize=wsize, tstep=tstep, maxit=1000, tol=0.0001, debias=False, verbose=False)
assert_allclose(X_hat_tf, X_hat_bcd, rtol=0.001)
assert_array_equal(np.where(active_set)[0], true_active_set)
alpha_space = 50.0
X_hat_bcd, active_set, _ = iterative_tf_mixed_norm_solver(M, G, alpha_space, alpha_time, 3, wsize=wsize, tstep=tstep, n_orient=5, maxit=1000, tol=0.0001, debias=False, verbose=False)
assert_array_equal(np.where(active_set)[0], [0, 1, 2, 3, 4])
alpha_space = 40.0
X_hat_bcd, active_set, _ = iterative_tf_mixed_norm_solver(M, G, alpha_space, alpha_time, 2, wsize=wsize, tstep=tstep, n_orient=2, maxit=1000, tol=0.0001, debias=False, verbose=False)
assert_array_equal(np.where(active_set)[0], [0, 1, 4, 5])
```

## Next Steps


---

*Source: test_mxne_optim.py:448 | Complexity: Advanced | Last updated: 2026-05-18*