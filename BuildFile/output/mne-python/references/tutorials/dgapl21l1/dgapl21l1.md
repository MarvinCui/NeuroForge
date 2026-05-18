# How To: Dgapl21L1

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test duality gap for L21 + L1 regularization.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.inverse_sparse.mxne_optim`
- `mne.time_frequency._stft`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test duality gap for L21 + L1 regularization.'

```python
'Test duality gap for L21 + L1 regularization.'
```

**Verification:**
```python
assert_allclose(0.0, gap)
```

### Step 2: Assign n_orient = 2

```python
n_orient = 2
```

**Verification:**
```python
assert_array_less(-1e-10, gap)
```

### Step 3: Assign unknown = _generate_tf_data(...)

```python
M, G, active_set = _generate_tf_data()
```

**Verification:**
```python
assert_array_less(gap, 1e-08)
```

### Step 4: Assign n_times = value

```python
n_times = M.shape[1]
```

**Verification:**
```python
assert_array_less(1, len(active_set_hat_tf))
```

### Step 5: Assign n_sources = value

```python
n_sources = G.shape[1]
```

**Verification:**
```python
assert_array_less(-1e-10, gap)
```

### Step 6: Assign unknown = value

```python
tstep, wsize = (np.array([4, 2]), np.array([64, 16]))
```

**Verification:**
```python
assert_array_less(gap, 1e-08)
```

### Step 7: Assign n_steps = np.ceil.astype(...)

```python
n_steps = np.ceil(n_times / tstep.astype(float)).astype(int)
```

**Verification:**
```python
assert_array_less(1, len(active_set_hat_tf))
```

### Step 8: Assign n_freqs = value

```python
n_freqs = wsize // 2 + 1
```

### Step 9: Assign n_coefs = value

```python
n_coefs = n_steps * n_freqs
```

### Step 10: Assign phi = _Phi(...)

```python
phi = _Phi(wsize, tstep, n_coefs, n_times)
```

### Step 11: Assign phiT = _PhiT(...)

```python
phiT = _PhiT(tstep, n_freqs, n_steps, n_times)
```

### Step 12: Assign alpha_max = norm_epsilon_inf(...)

```python
alpha_max = norm_epsilon_inf(G, M, phi, l1_ratio, n_orient)
```

### Step 13: Assign alpha_space = value

```python
alpha_space = (1.0 - l1_ratio) * alpha_max
```

### Step 14: Assign alpha_time = value

```python
alpha_time = l1_ratio * alpha_max
```

### Step 15: Assign Z = np.zeros(...)

```python
Z = np.zeros([n_sources, phi.n_coefs.sum()])
```

### Step 16: Assign gap = value

```python
gap = dgap_l21l1(M, G, Z, np.ones(n_sources, dtype=bool), alpha_space, alpha_time, phi, phiT, n_orient, -np.inf)[0]
```

### Step 17: Call assert_allclose()

```python
assert_allclose(0.0, gap)
```

### Step 18: Assign unknown = tf_mixed_norm_solver(...)

```python
X_hat_tf, active_set_hat_tf, E, gap = tf_mixed_norm_solver(M, G, alpha_space / 1.01, alpha_time / 1.01, maxit=200, tol=1e-08, verbose=True, debias=False, n_orient=n_orient, tstep=tstep, wsize=wsize, return_gap=True)
```

### Step 19: Call assert_array_less()

```python
assert_array_less(-1e-10, gap)
```

### Step 20: Call assert_array_less()

```python
assert_array_less(gap, 1e-08)
```

### Step 21: Call assert_array_less()

```python
assert_array_less(1, len(active_set_hat_tf))
```

### Step 22: Assign unknown = tf_mixed_norm_solver(...)

```python
X_hat_tf, active_set_hat_tf, E, gap = tf_mixed_norm_solver(M, G, alpha_space / 5.0, alpha_time / 5.0, maxit=200, tol=1e-08, verbose=True, debias=False, n_orient=n_orient, tstep=tstep, wsize=wsize, return_gap=True)
```

### Step 23: Call assert_array_less()

```python
assert_array_less(-1e-10, gap)
```

### Step 24: Call assert_array_less()

```python
assert_array_less(gap, 1e-08)
```

### Step 25: Call assert_array_less()

```python
assert_array_less(1, len(active_set_hat_tf))
```


## Complete Example

```python
# Workflow
'Test duality gap for L21 + L1 regularization.'
n_orient = 2
M, G, active_set = _generate_tf_data()
n_times = M.shape[1]
n_sources = G.shape[1]
tstep, wsize = (np.array([4, 2]), np.array([64, 16]))
n_steps = np.ceil(n_times / tstep.astype(float)).astype(int)
n_freqs = wsize // 2 + 1
n_coefs = n_steps * n_freqs
phi = _Phi(wsize, tstep, n_coefs, n_times)
phiT = _PhiT(tstep, n_freqs, n_steps, n_times)
for l1_ratio in [0.05, 0.1]:
    alpha_max = norm_epsilon_inf(G, M, phi, l1_ratio, n_orient)
    alpha_space = (1.0 - l1_ratio) * alpha_max
    alpha_time = l1_ratio * alpha_max
    Z = np.zeros([n_sources, phi.n_coefs.sum()])
    gap = dgap_l21l1(M, G, Z, np.ones(n_sources, dtype=bool), alpha_space, alpha_time, phi, phiT, n_orient, -np.inf)[0]
    assert_allclose(0.0, gap)
    X_hat_tf, active_set_hat_tf, E, gap = tf_mixed_norm_solver(M, G, alpha_space / 1.01, alpha_time / 1.01, maxit=200, tol=1e-08, verbose=True, debias=False, n_orient=n_orient, tstep=tstep, wsize=wsize, return_gap=True)
    assert_array_less(-1e-10, gap)
    assert_array_less(gap, 1e-08)
    assert_array_less(1, len(active_set_hat_tf))
    X_hat_tf, active_set_hat_tf, E, gap = tf_mixed_norm_solver(M, G, alpha_space / 5.0, alpha_time / 5.0, maxit=200, tol=1e-08, verbose=True, debias=False, n_orient=n_orient, tstep=tstep, wsize=wsize, return_gap=True)
    assert_array_less(-1e-10, gap)
    assert_array_less(gap, 1e-08)
    assert_array_less(1, len(active_set_hat_tf))
```

## Next Steps


---

*Source: test_mxne_optim.py:218 | Complexity: Advanced | Last updated: 2026-05-18*