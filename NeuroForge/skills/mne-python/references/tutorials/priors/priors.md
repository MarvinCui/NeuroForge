# How To: Priors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test prior computations.

## Prerequisites

**Required Modules:**
- `gc`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.channels`
- `mne.datasets`
- `mne.forward`
- `mne.io`
- `mne.label`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test prior computations.'

```python
'Test prior computations.'
```

**Verification:**
```python
assert not is_fixed_orient(fwd)
```

### Step 2: Assign fwd = read_forward_solution(...)

```python
fwd = read_forward_solution(fname_meeg)
```

**Verification:**
```python
assert depth_prior.shape == (3 * n_sources,)
```

### Step 3: Assign n_sources = value

```python
n_sources = fwd['nsource']
```

**Verification:**
```python
assert_array_equal(depth_prior, 1.0)
```

### Step 4: Assign info = read_info(...)

```python
info = read_info(fname_evoked)
```

**Verification:**
```python
assert depth_prior.shape == (n_sources,)
```

### Step 5: Assign depth_prior = compute_depth_prior(...)

```python
depth_prior = compute_depth_prior(fwd, info, exp=0.8)
```

**Verification:**
```python
assert_array_equal(orient_prior, 1.0)
```

### Step 6: Assign depth_prior = compute_depth_prior(...)

```python
depth_prior = compute_depth_prior(fwd, info, exp=0.0)
```

**Verification:**
```python
assert_array_equal(orient_prior, 1.0)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(depth_prior, 1.0)
```

**Verification:**
```python
assert all(np.isin(orient_prior, (0.5, 1.0)))
```

### Step 8: Assign fwd_fixed = convert_forward_solution(...)

```python
fwd_fixed = convert_forward_solution(fwd, force_fixed=True)
```

### Step 9: Assign depth_prior = compute_depth_prior(...)

```python
depth_prior = compute_depth_prior(fwd_fixed, info=info)
```

**Verification:**
```python
assert depth_prior.shape == (n_sources,)
```

### Step 10: Assign orient_prior = compute_orient_prior(...)

```python
orient_prior = compute_orient_prior(fwd, 1.0)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(orient_prior, 1.0)
```

### Step 12: Assign orient_prior = compute_orient_prior(...)

```python
orient_prior = compute_orient_prior(fwd_fixed, 0.0)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(orient_prior, 1.0)
```

### Step 14: Assign fwd_surf_ori = convert_forward_solution(...)

```python
fwd_surf_ori = convert_forward_solution(fwd, surf_ori=True)
```

### Step 15: Assign orient_prior = compute_orient_prior(...)

```python
orient_prior = compute_orient_prior(fwd_surf_ori, 0.5)
```

**Verification:**
```python
assert all(np.isin(orient_prior, (0.5, 1.0)))
```

### Step 16: Call compute_depth_prior()

```python
compute_depth_prior(fwd, info, limit_depth_chs='foo')
```

### Step 17: Call compute_depth_prior()

```python
compute_depth_prior(fwd, info, limit_depth_chs='whiten')
```

### Step 18: Call compute_orient_prior()

```python
compute_orient_prior(fwd, 0.5)
```

### Step 19: Call compute_orient_prior()

```python
compute_orient_prior(fwd_surf_ori, -0.5)
```

### Step 20: Call compute_orient_prior()

```python
compute_orient_prior(fwd_fixed, 0.5)
```


## Complete Example

```python
# Workflow
'Test prior computations.'
fwd = read_forward_solution(fname_meeg)
assert not is_fixed_orient(fwd)
n_sources = fwd['nsource']
info = read_info(fname_evoked)
depth_prior = compute_depth_prior(fwd, info, exp=0.8)
assert depth_prior.shape == (3 * n_sources,)
depth_prior = compute_depth_prior(fwd, info, exp=0.0)
assert_array_equal(depth_prior, 1.0)
with pytest.raises(ValueError, match='must be "whiten"'):
    compute_depth_prior(fwd, info, limit_depth_chs='foo')
with pytest.raises(ValueError, match='noise_cov must be a Covariance'):
    compute_depth_prior(fwd, info, limit_depth_chs='whiten')
fwd_fixed = convert_forward_solution(fwd, force_fixed=True)
depth_prior = compute_depth_prior(fwd_fixed, info=info)
assert depth_prior.shape == (n_sources,)
orient_prior = compute_orient_prior(fwd, 1.0)
assert_array_equal(orient_prior, 1.0)
orient_prior = compute_orient_prior(fwd_fixed, 0.0)
assert_array_equal(orient_prior, 1.0)
with pytest.raises(ValueError, match='oriented in surface coordinates'):
    compute_orient_prior(fwd, 0.5)
fwd_surf_ori = convert_forward_solution(fwd, surf_ori=True)
orient_prior = compute_orient_prior(fwd_surf_ori, 0.5)
assert all(np.isin(orient_prior, (0.5, 1.0)))
with pytest.raises(ValueError, match='between 0 and 1'):
    compute_orient_prior(fwd_surf_ori, -0.5)
with pytest.raises(ValueError, match='with fixed orientation'):
    compute_orient_prior(fwd_fixed, 0.5)
```

## Next Steps


---

*Source: test_forward.py:486 | Complexity: Advanced | Last updated: 2026-05-18*