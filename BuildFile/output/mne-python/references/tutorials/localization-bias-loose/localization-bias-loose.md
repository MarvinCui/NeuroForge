# How To: Localization Bias Loose

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test inverse localization bias for loose minimum-norm solvers.

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
# Fixtures: bias_params_fixed, method, lower, upper, depth, loose, pick_ori
```

## Step-by-Step Guide

### Step 1: 'Test inverse localization bias for loose minimum-norm solvers.'

```python
'Test inverse localization bias for loose minimum-norm solvers.'
```

**Verification:**
```python
assert not is_fixed_orient(fwd)
```

### Step 2: Assign unknown = bias_params_fixed

```python
evoked, fwd, noise_cov, _, want = bias_params_fixed
```

**Verification:**
```python
assert loc.data.ndim == 3
```

### Step 3: Assign fwd = convert_forward_solution(...)

```python
fwd = convert_forward_solution(fwd, surf_ori=False, force_fixed=False)
```

**Verification:**
```python
assert np.percentile(abs_cos_sim, 10) > 0.9
```

### Step 4: Assign inv_loose = make_inverse_operator(...)

```python
inv_loose = make_inverse_operator(evoked.info, fwd, noise_cov, loose=loose, depth=depth)
```

**Verification:**
```python
assert (loc >= 0).all()
```

### Step 5: Assign unknown = apply_inverse(...)

```python
loc, res = apply_inverse(evoked, inv_loose, lambda2, method, pick_ori=pick_ori, return_residual=True)
```

**Verification:**
```python
assert lower <= perc <= upper, method
```

### Step 6: Assign perc = value

```python
perc = (want == np.argmax(loc, axis=0)).mean() * 100
```

**Verification:**
```python
assert lower <= perc <= upper, method
```

### Step 7: Assign unknown = loc.project(...)

```python
loc, directions = loc.project('pca', src=fwd['src'])
```

### Step 8: Assign abs_cos_sim = np.abs(...)

```python
abs_cos_sim = np.abs(np.sum(directions * inv_loose['source_nn'][2::3], axis=1))
```

**Verification:**
```python
assert np.percentile(abs_cos_sim, 10) > 0.9
```

### Step 9: Assign loc = value

```python
loc = abs(loc).data
```

### Step 10: Assign loc = value

```python
loc = loc.data
```


## Complete Example

```python
# Setup
# Fixtures: bias_params_fixed, method, lower, upper, depth, loose, pick_ori

# Workflow
'Test inverse localization bias for loose minimum-norm solvers.'
if pick_ori == 'vector' and method == 'eLORETA':
    return
evoked, fwd, noise_cov, _, want = bias_params_fixed
fwd = convert_forward_solution(fwd, surf_ori=False, force_fixed=False)
assert not is_fixed_orient(fwd)
inv_loose = make_inverse_operator(evoked.info, fwd, noise_cov, loose=loose, depth=depth)
loc, res = apply_inverse(evoked, inv_loose, lambda2, method, pick_ori=pick_ori, return_residual=True)
if pick_ori is not None:
    assert loc.data.ndim == 3
    loc, directions = loc.project('pca', src=fwd['src'])
    abs_cos_sim = np.abs(np.sum(directions * inv_loose['source_nn'][2::3], axis=1))
    assert np.percentile(abs_cos_sim, 10) > 0.9
    loc = abs(loc).data
else:
    loc = loc.data
assert (loc >= 0).all()
perc = (want == np.argmax(loc, axis=0)).mean() * 100
assert lower <= perc <= upper, method
```

## Next Steps


---

*Source: test_inverse.py:462 | Complexity: Advanced | Last updated: 2026-05-18*