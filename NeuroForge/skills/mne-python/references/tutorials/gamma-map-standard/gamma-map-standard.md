# How To: Gamma Map Standard

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test Gamma MAP inverse.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne.cov`
- `mne.datasets`
- `mne.dipole`
- `mne.inverse_sparse`
- `mne.inverse_sparse.mxne_inverse`
- `mne.minimum_norm.tests.test_inverse`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test Gamma MAP inverse.'

```python
'Test Gamma MAP inverse.'
```

**Verification:**
```python
assert_var_exp_log(log.getvalue(), 20, 22)
```

### Step 2: Assign forward = read_forward_solution(...)

```python
forward = read_forward_solution(fname_fwd)
```

**Verification:**
```python
assert_var_exp_log(log.getvalue(), 20, 22)
```

### Step 3: Assign forward = convert_forward_solution(...)

```python
forward = convert_forward_solution(forward, surf_ori=True)
```

**Verification:**
```python
assert_stcs_equal(stc_vec.magnitude(), stc)
```

### Step 4: Assign forward = pick_types_forward(...)

```python
forward = pick_types_forward(forward, meg=False, eeg=True)
```

**Verification:**
```python
assert_allclose(exp_var, dip_exp_var, atol=10)
```

### Step 5: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(fname_evoked, condition=0, baseline=(None, 0), proj=False)
```

**Verification:**
```python
assert isinstance(dips[0], Dipole)
```

### Step 6: Call evoked.resample()

```python
evoked.resample(50, npad=100)
```

**Verification:**
```python
assert_stcs_equal(stc.magnitude(), stc_dip)
```

### Step 7: Call evoked.crop()

```python
evoked.crop(tmin=0.1, tmax=0.14)
```

### Step 8: Assign cov = read_cov(...)

```python
cov = read_cov(fname_cov)
```

### Step 9: Assign cov = regularize(...)

```python
cov = regularize(cov, evoked.info)
```

### Step 10: Assign alpha = 0.5

```python
alpha = 0.5
```

### Step 11: Call _check_stc()

```python
_check_stc(stc, evoked, 68477, 'lh', fwd=forward)
```

### Step 12: Call assert_var_exp_log()

```python
assert_var_exp_log(log.getvalue(), 20, 22)
```

### Step 13: Call assert_var_exp_log()

```python
assert_var_exp_log(log.getvalue(), 20, 22)
```

### Step 14: Call assert_stcs_equal()

```python
assert_stcs_equal(stc_vec.magnitude(), stc)
```

### Step 15: Call _check_stc()

```python
_check_stc(stc_vec, evoked, 68477, 'lh', fwd=forward, res=res)
```

### Step 16: Assign unknown = gamma_map(...)

```python
stc, res = gamma_map(evoked, forward, cov, alpha, tol=0.0001, xyz_same_gamma=False, update_mode=1, pick_ori='vector', return_residual=True)
```

### Step 17: Call _check_stc()

```python
_check_stc(stc, evoked, 82010, 'lh', fwd=forward, dist_limit=6.0, ratio=2.0, res=res)
```

### Step 18: Assign exp_var = assert_var_exp_log(...)

```python
exp_var = assert_var_exp_log(log.getvalue(), 58, 60)
```

### Step 19: Assign dip_exp_var = np.mean(...)

```python
dip_exp_var = np.mean(sum((dip.gof for dip in dips)))
```

### Step 20: Call assert_allclose()

```python
assert_allclose(exp_var, dip_exp_var, atol=10)
```

**Verification:**
```python
assert isinstance(dips[0], Dipole)
```

### Step 21: Assign stc_dip = make_stc_from_dipoles(...)

```python
stc_dip = make_stc_from_dipoles(dips, forward['src'])
```

### Step 22: Call assert_stcs_equal()

```python
assert_stcs_equal(stc.magnitude(), stc_dip)
```

### Step 23: Assign unknown = gamma_map(...)

```python
stc, res = gamma_map(evoked, forward, cov, alpha, tol=0.0001, xyz_same_gamma=False, update_mode=2, loose=0, return_residual=True)
```

### Step 24: Call _check_stc()

```python
_check_stc(stc, evoked, 85739, 'lh', fwd=forward, ratio=20.0, res=res)
```

### Step 25: Assign stc = gamma_map(...)

```python
stc = gamma_map(evoked, forward, cov, alpha, tol=0.0001, xyz_same_gamma=True, update_mode=1, verbose=True)
```

### Step 26: Assign unknown = gamma_map(...)

```python
stc_vec, res = gamma_map(evoked, forward, cov, alpha, tol=0.0001, xyz_same_gamma=True, update_mode=1, pick_ori='vector', return_residual=True, verbose=True)
```

### Step 27: Assign dips = gamma_map(...)

```python
dips = gamma_map(evoked, forward, cov, alpha, tol=0.0001, xyz_same_gamma=False, update_mode=1, return_as_dipoles=True, verbose=True)
```


## Complete Example

```python
# Workflow
'Test Gamma MAP inverse.'
forward = read_forward_solution(fname_fwd)
forward = convert_forward_solution(forward, surf_ori=True)
forward = pick_types_forward(forward, meg=False, eeg=True)
evoked = read_evokeds(fname_evoked, condition=0, baseline=(None, 0), proj=False)
evoked.resample(50, npad=100)
evoked.crop(tmin=0.1, tmax=0.14)
cov = read_cov(fname_cov)
cov = regularize(cov, evoked.info)
alpha = 0.5
with catch_logging() as log:
    stc = gamma_map(evoked, forward, cov, alpha, tol=0.0001, xyz_same_gamma=True, update_mode=1, verbose=True)
_check_stc(stc, evoked, 68477, 'lh', fwd=forward)
assert_var_exp_log(log.getvalue(), 20, 22)
with catch_logging() as log:
    stc_vec, res = gamma_map(evoked, forward, cov, alpha, tol=0.0001, xyz_same_gamma=True, update_mode=1, pick_ori='vector', return_residual=True, verbose=True)
assert_var_exp_log(log.getvalue(), 20, 22)
assert_stcs_equal(stc_vec.magnitude(), stc)
_check_stc(stc_vec, evoked, 68477, 'lh', fwd=forward, res=res)
stc, res = gamma_map(evoked, forward, cov, alpha, tol=0.0001, xyz_same_gamma=False, update_mode=1, pick_ori='vector', return_residual=True)
_check_stc(stc, evoked, 82010, 'lh', fwd=forward, dist_limit=6.0, ratio=2.0, res=res)
with catch_logging() as log:
    dips = gamma_map(evoked, forward, cov, alpha, tol=0.0001, xyz_same_gamma=False, update_mode=1, return_as_dipoles=True, verbose=True)
exp_var = assert_var_exp_log(log.getvalue(), 58, 60)
dip_exp_var = np.mean(sum((dip.gof for dip in dips)))
assert_allclose(exp_var, dip_exp_var, atol=10)
assert isinstance(dips[0], Dipole)
stc_dip = make_stc_from_dipoles(dips, forward['src'])
assert_stcs_equal(stc.magnitude(), stc_dip)
stc, res = gamma_map(evoked, forward, cov, alpha, tol=0.0001, xyz_same_gamma=False, update_mode=2, loose=0, return_residual=True)
_check_stc(stc, evoked, 85739, 'lh', fwd=forward, ratio=20.0, res=res)
```

## Next Steps


---

*Source: test_gamma_map.py:61 | Complexity: Advanced | Last updated: 2026-05-18*