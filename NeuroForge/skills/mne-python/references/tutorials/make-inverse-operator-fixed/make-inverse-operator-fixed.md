# How To: Make Inverse Operator Fixed

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test MNE inverse computation (fixed orientation).

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
# Fixtures: evoked, noise_cov
```

## Step-by-Step Guide

### Step 1: 'Test MNE inverse computation (fixed orientation).'

```python
'Test MNE inverse computation (fixed orientation).'
```

**Verification:**
```python
assert 'MEG: rank 302 computed from 305' in log
```

### Step 2: Assign fwd = read_forward_solution_meg(...)

```python
fwd = read_forward_solution_meg(fname_fwd)
```

**Verification:**
```python
assert 'EEG channels: 0' in repr(inv_op)
```

### Step 3: Assign fwd_fixed = convert_forward_solution(...)

```python
fwd_fixed = convert_forward_solution(fwd, force_fixed=True, use_cps=True)
```

**Verification:**
```python
assert 'MEG channels: 305' in repr(inv_op)
```

### Step 4: Call pytest.raises()

```python
pytest.raises(ValueError, make_inverse_operator, evoked.info, fwd_fixed, noise_cov, depth=0.8, fixed=True)
```

**Verification:**
```python
assert 'Fixed' in repr(inv_op)
```

### Step 5: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'MEG channels: 305' in repr(inverse_operator_nodepth)
```

### Step 6: Assign inverse_operator_nodepth = read_inverse_operator(...)

```python
inverse_operator_nodepth = read_inverse_operator(fname_inv_fixed_nodepth)
```

**Verification:**
```python
assert compute_rank_inverse(inverse_operator_nodepth) == 302
```

### Step 7: Call _compare_inverses_approx()

```python
_compare_inverses_approx(inverse_operator_nodepth, inv_op, evoked, rtol=1e-05, atol=0.0001)
```

**Verification:**
```python
assert_allclose(inverse_operator_depth['source_nn'], fwd_surf['source_nn'][2::3], atol=1e-05)
```

### Step 8: Assign fwd_surf = convert_forward_solution(...)

```python
fwd_surf = convert_forward_solution(fwd, surf_ori=True)
```

### Step 9: Assign inv_op = make_inverse_operator(...)

```python
inv_op = make_inverse_operator(evoked.info, fwd, noise_cov, depth=0.0, fixed=True, use_cps=False, verbose=True)
```

### Step 10: Assign inv_op_depth = make_inverse_operator(...)

```python
inv_op_depth = make_inverse_operator(evoked.info, use_fwd, noise_cov, depth=0.8, use_cps=True, **kwargs)
```

### Step 11: Assign inverse_operator_depth = read_inverse_operator(...)

```python
inverse_operator_depth = read_inverse_operator(fname_inv_fixed_depth)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(inverse_operator_depth['source_nn'], fwd_surf['source_nn'][2::3], atol=1e-05)
```

### Step 13: Call _compare_inverses_approx()

```python
_compare_inverses_approx(inverse_operator_depth, inv_op_depth, evoked, rtol=0.001, atol=0.0001)
```


## Complete Example

```python
# Setup
# Fixtures: evoked, noise_cov

# Workflow
'Test MNE inverse computation (fixed orientation).'
fwd = read_forward_solution_meg(fname_fwd)
fwd_fixed = convert_forward_solution(fwd, force_fixed=True, use_cps=True)
pytest.raises(ValueError, make_inverse_operator, evoked.info, fwd_fixed, noise_cov, depth=0.8, fixed=True)
with catch_logging() as log:
    inv_op = make_inverse_operator(evoked.info, fwd, noise_cov, depth=0.0, fixed=True, use_cps=False, verbose=True)
log = log.getvalue()
assert 'MEG: rank 302 computed from 305' in log
assert 'EEG channels: 0' in repr(inv_op)
assert 'MEG channels: 305' in repr(inv_op)
assert 'Fixed' in repr(inv_op)
del fwd_fixed
inverse_operator_nodepth = read_inverse_operator(fname_inv_fixed_nodepth)
assert 'MEG channels: 305' in repr(inverse_operator_nodepth)
_compare_inverses_approx(inverse_operator_nodepth, inv_op, evoked, rtol=1e-05, atol=0.0001)
assert compute_rank_inverse(inverse_operator_nodepth) == 302
fwd_surf = convert_forward_solution(fwd, surf_ori=True)
for kwargs, use_fwd in zip([dict(fixed=True), dict(loose=0.0)], [fwd, fwd_surf]):
    inv_op_depth = make_inverse_operator(evoked.info, use_fwd, noise_cov, depth=0.8, use_cps=True, **kwargs)
    inverse_operator_depth = read_inverse_operator(fname_inv_fixed_depth)
    assert_allclose(inverse_operator_depth['source_nn'], fwd_surf['source_nn'][2::3], atol=1e-05)
    _compare_inverses_approx(inverse_operator_depth, inv_op_depth, evoked, rtol=0.001, atol=0.0001)
```

## Next Steps


---

*Source: test_inverse.py:849 | Complexity: Advanced | Last updated: 2026-05-18*