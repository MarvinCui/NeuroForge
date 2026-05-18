# How To: Inverse Residual

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test MNE inverse application.

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
# Fixtures: evoked, method, pick_ori
```

## Step-by-Step Guide

### Step 1: 'Test MNE inverse application.'

```python
'Test MNE inverse application.'
```

**Verification:**
```python
assert_array_equal(residual.data.real, 0)
```

### Step 2: Assign evoked = evoked.pick(...)

```python
evoked = evoked.pick('meg', exclude='bads')
```

**Verification:**
```python
assert stc.data.min() < 0
```

### Step 3: Assign fwd = read_forward_solution(...)

```python
fwd = read_forward_solution(fname_fwd)
```

**Verification:**
```python
assert_var_exp_log(log.getvalue(), 45, 52)
```

### Step 4: Call pick_channels_forward()

```python
pick_channels_forward(fwd, evoked.ch_names, copy=False)
```

**Verification:**
```python
assert_stc_res(evoked, stc, fwd, residual, atol=1e-16)
```

### Step 5: Assign fwd = convert_forward_solution(...)

```python
fwd = convert_forward_solution(fwd, force_fixed=True, surf_ori=True)
```

**Verification:**
```python
assert_var_exp_log(log.getvalue(), 100, 100)
```

### Step 6: Assign evoked.data = value

```python
evoked.data = 1j * evoked.data
```

**Verification:**
```python
assert_array_less(np.abs(residual.data), 1e-15)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(residual.data.real, 0)
```

### Step 8: Assign residual.data = value

```python
residual.data = (-1j * residual.data).real
```

### Step 9: Assign evoked.data = value

```python
evoked.data = (-1j * evoked.data).real
```

**Verification:**
```python
assert stc.data.min() < 0
```

### Step 10: Assign stc.data = value

```python
stc.data = -1j * stc.data
```

### Step 11: Call assert_var_exp_log()

```python
assert_var_exp_log(log.getvalue(), 45, 52)
```

### Step 12: Assign inv = read_inverse_operator(...)

```python
inv = read_inverse_operator(fname_inv_fixed_depth)
```

### Step 13: Assign inv = read_inverse_operator(...)

```python
inv = read_inverse_operator(fname_inv)
```

### Step 14: Assign unknown = apply_inverse(...)

```python
stc, residual = apply_inverse(evoked, inv, method=method, return_residual=True, verbose=True, pick_ori=pick_ori)
```

### Step 15: Call assert_stc_res()

```python
assert_stc_res(evoked, stc, fwd, residual, atol=1e-16)
```

### Step 16: Call assert_var_exp_log()

```python
assert_var_exp_log(log.getvalue(), 100, 100)
```

### Step 17: Call assert_array_less()

```python
assert_array_less(np.abs(residual.data), 1e-15)
```

### Step 18: Assign unknown = apply_inverse(...)

```python
_, residual = apply_inverse(evoked, inv, 0.0, method, return_residual=True, verbose=True)
```


## Complete Example

```python
# Setup
# Fixtures: evoked, method, pick_ori

# Workflow
'Test MNE inverse application.'
if method == 'eLORETA' and pick_ori == 'vector':
    return
evoked = evoked.pick('meg', exclude='bads')
if pick_ori is None:
    inv = read_inverse_operator(fname_inv_fixed_depth)
else:
    inv = read_inverse_operator(fname_inv)
fwd = read_forward_solution(fname_fwd)
pick_channels_forward(fwd, evoked.ch_names, copy=False)
fwd = convert_forward_solution(fwd, force_fixed=True, surf_ori=True)
evoked.data = 1j * evoked.data
with catch_logging() as log:
    stc, residual = apply_inverse(evoked, inv, method=method, return_residual=True, verbose=True, pick_ori=pick_ori)
assert_array_equal(residual.data.real, 0)
residual.data = (-1j * residual.data).real
evoked.data = (-1j * evoked.data).real
assert stc.data.min() < 0
stc.data = -1j * stc.data
assert_var_exp_log(log.getvalue(), 45, 52)
if method not in ('dSPM', 'sLORETA'):
    assert_stc_res(evoked, stc, fwd, residual, atol=1e-16)
if method != 'sLORETA':
    with catch_logging() as log:
        _, residual = apply_inverse(evoked, inv, 0.0, method, return_residual=True, verbose=True)
    assert_var_exp_log(log.getvalue(), 100, 100)
    assert_array_less(np.abs(residual.data), 1e-15)
```

## Next Steps


---

*Source: test_inverse.py:805 | Complexity: Advanced | Last updated: 2026-05-18*