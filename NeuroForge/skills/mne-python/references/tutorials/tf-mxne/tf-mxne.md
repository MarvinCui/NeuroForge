# How To: Tf Mxne

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test convergence of TF-MxNE solver.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.inverse_sparse.mxne_optim`
- `mne.time_frequency._stft`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test convergence of TF-MxNE solver.'

```python
'Test convergence of TF-MxNE solver.'
```

**Verification:**
```python
assert_array_less(gap_tfmxne, 1e-08)
```

### Step 2: Assign alpha_space = 10.0

```python
alpha_space = 10.0
```

**Verification:**
```python
assert_array_equal(np.where(active_set_hat_tf)[0], active_set)
```

### Step 3: Assign alpha_time = 5.0

```python
alpha_time = 5.0
```

### Step 4: Assign unknown = _generate_tf_data(...)

```python
M, G, active_set = _generate_tf_data()
```

### Step 5: Call assert_array_less()

```python
assert_array_less(gap_tfmxne, 1e-08)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(np.where(active_set_hat_tf)[0], active_set)
```

### Step 7: Assign unknown = tf_mixed_norm_solver(...)

```python
X_hat_tf, active_set_hat_tf, E, gap_tfmxne = tf_mixed_norm_solver(M, G, alpha_space, alpha_time, maxit=200, tol=1e-08, verbose=True, n_orient=1, tstep=4, wsize=32, return_gap=True)
```


## Complete Example

```python
# Workflow
'Test convergence of TF-MxNE solver.'
alpha_space = 10.0
alpha_time = 5.0
M, G, active_set = _generate_tf_data()
with _record_warnings():
    X_hat_tf, active_set_hat_tf, E, gap_tfmxne = tf_mixed_norm_solver(M, G, alpha_space, alpha_time, maxit=200, tol=1e-08, verbose=True, n_orient=1, tstep=4, wsize=32, return_gap=True)
assert_array_less(gap_tfmxne, 1e-08)
assert_array_equal(np.where(active_set_hat_tf)[0], active_set)
```

## Next Steps


---

*Source: test_mxne_optim.py:143 | Complexity: Intermediate | Last updated: 2026-05-18*