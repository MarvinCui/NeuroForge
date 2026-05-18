# How To: Make Inverse Operator Loose

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test MNE inverse computation (precomputed and non-precomputed).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `re`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne.channels`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.fixes`
- `mne.forward`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.time_frequency`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: evoked, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test MNE inverse computation (precomputed and non-precomputed).'

```python
'Test MNE inverse computation (precomputed and non-precomputed).'
```

**Verification:**
```python
assert 'MEG: rank 302 computed' in log
```

### Step 2: Assign noise_cov = read_cov(...)

```python
noise_cov = read_cov(fname_cov)
```

**Verification:**
```python
assert f"limit = 1/{fwd_op['nsource']}" in log
```

### Step 3: Assign inverse_operator = read_inverse_operator(...)

```python
inverse_operator = read_inverse_operator(fname_inv)
```

**Verification:**
```python
assert 'Loose (0.2)' in repr(my_inv_op)
```

### Step 4: Assign fwd_op = convert_forward_solution(...)

```python
fwd_op = convert_forward_solution(read_forward_solution_meg(fname_fwd), surf_ori=True, copy=False)
```

**Verification:**
```python
assert_equal(inverse_operator['units'], 'Am')
```

### Step 5: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'MEG: rank 302 computed from 305' in log
```

### Step 6: Call _compare_io()

```python
_compare_io(my_inv_op, tmp_path=tmp_path)
```

**Verification:**
```python
assert 'dev_head_t' in my_inv_op['info']
```

### Step 7: Call assert_equal()

```python
assert_equal(inverse_operator['units'], 'Am')
```

**Verification:**
```python
assert 'mri_head_t' in my_inv_op
```

### Step 8: Call _compare_inverses_approx()

```python
_compare_inverses_approx(my_inv_op, inverse_operator, evoked, rtol=0.01, atol=1e-05, depth_atol=0.001)
```

### Step 9: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'MEG: rank 302 computed from 305' in log
```

### Step 10: Call _compare_io()

```python
_compare_io(my_inv_op, tmp_path=tmp_path)
```

### Step 11: Call _compare_inverses_approx()

```python
_compare_inverses_approx(my_inv_op, inverse_operator, evoked, rtol=0.001, atol=1e-05)
```

**Verification:**
```python
assert 'dev_head_t' in my_inv_op['info']
```

### Step 12: Assign my_inv_op = make_inverse_operator(...)

```python
my_inv_op = make_inverse_operator(evoked.info, fwd_op, noise_cov, loose=0.2, depth=dict(exp=0.8, limit_depth_chs=False), verbose=True)
```

### Step 13: Assign my_inv_op = make_inverse_operator(...)

```python
my_inv_op = make_inverse_operator(evoked.info, fwd_op, noise_cov, loose='auto', depth=0.8, fixed=False, verbose=True)
```


## Complete Example

```python
# Setup
# Fixtures: evoked, tmp_path

# Workflow
'Test MNE inverse computation (precomputed and non-precomputed).'
noise_cov = read_cov(fname_cov)
inverse_operator = read_inverse_operator(fname_inv)
fwd_op = convert_forward_solution(read_forward_solution_meg(fname_fwd), surf_ori=True, copy=False)
with catch_logging() as log:
    my_inv_op = make_inverse_operator(evoked.info, fwd_op, noise_cov, loose=0.2, depth=dict(exp=0.8, limit_depth_chs=False), verbose=True)
log = log.getvalue()
assert 'MEG: rank 302 computed' in log
assert f"limit = 1/{fwd_op['nsource']}" in log
assert 'Loose (0.2)' in repr(my_inv_op)
_compare_io(my_inv_op, tmp_path=tmp_path)
assert_equal(inverse_operator['units'], 'Am')
_compare_inverses_approx(my_inv_op, inverse_operator, evoked, rtol=0.01, atol=1e-05, depth_atol=0.001)
with catch_logging() as log:
    my_inv_op = make_inverse_operator(evoked.info, fwd_op, noise_cov, loose='auto', depth=0.8, fixed=False, verbose=True)
log = log.getvalue()
assert 'MEG: rank 302 computed from 305' in log
_compare_io(my_inv_op, tmp_path=tmp_path)
_compare_inverses_approx(my_inv_op, inverse_operator, evoked, rtol=0.001, atol=1e-05)
assert 'dev_head_t' in my_inv_op['info']
assert 'mri_head_t' in my_inv_op
```

## Next Steps


---

*Source: test_inverse.py:294 | Complexity: Advanced | Last updated: 2026-05-18*