# How To: Tf Mxne Vs Mxne

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test equivalence of TF-MxNE (with alpha_time=0) and MxNE.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.inverse_sparse.mxne_optim`
- `mne.time_frequency._stft`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test equivalence of TF-MxNE (with alpha_time=0) and MxNE.'

```python
'Test equivalence of TF-MxNE (with alpha_time=0) and MxNE.'
```

**Verification:**
```python
assert_allclose(X_hat_tf, X_hat_l21, rtol=0.1)
```

### Step 2: Assign alpha_space = 60.0

```python
alpha_space = 60.0
```

### Step 3: Assign alpha_time = 0.0

```python
alpha_time = 0.0
```

### Step 4: Assign unknown = _generate_tf_data(...)

```python
M, G, active_set = _generate_tf_data()
```

### Step 5: Assign unknown = tf_mixed_norm_solver(...)

```python
X_hat_tf, active_set_hat_tf, E = tf_mixed_norm_solver(M, G, alpha_space, alpha_time, maxit=200, tol=1e-08, verbose=True, debias=False, n_orient=1, tstep=4, wsize=32)
```

### Step 6: Assign unknown = mixed_norm_solver(...)

```python
X_hat_l21, _, _ = mixed_norm_solver(M, G, alpha_space, maxit=200, tol=1e-08, verbose=False, n_orient=1, active_set_size=None, debias=False)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(X_hat_tf, X_hat_l21, rtol=0.1)
```


## Complete Example

```python
# Workflow
'Test equivalence of TF-MxNE (with alpha_time=0) and MxNE.'
alpha_space = 60.0
alpha_time = 0.0
M, G, active_set = _generate_tf_data()
X_hat_tf, active_set_hat_tf, E = tf_mixed_norm_solver(M, G, alpha_space, alpha_time, maxit=200, tol=1e-08, verbose=True, debias=False, n_orient=1, tstep=4, wsize=32)
X_hat_l21, _, _ = mixed_norm_solver(M, G, alpha_space, maxit=200, tol=1e-08, verbose=False, n_orient=1, active_set_size=None, debias=False)
assert_allclose(X_hat_tf, X_hat_l21, rtol=0.1)
```

## Next Steps


---

*Source: test_mxne_optim.py:291 | Complexity: Intermediate | Last updated: 2026-05-18*