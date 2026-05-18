# How To: Apply Inverse Eloreta Mne Equiv

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that eLORETA with no iterations is the same as MNE.

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
# Fixtures: bias_params_free, loose, lambda2
```

## Step-by-Step Guide

### Step 1: 'Test that eLORETA with no iterations is the same as MNE.'

```python
'Test that eLORETA with no iterations is the same as MNE.'
```

**Verification:**
```python
assert 3e-09 < atol < 3e-06
```

### Step 2: Assign method_params = dict(...)

```python
method_params = dict(max_iter=0, force_equal=False)
```

**Verification:**
```python
assert_allclose(stc_mne.data, stc_e.data, atol=atol, rtol=0.0001)
```

### Step 3: Assign pick_ori = value

```python
pick_ori = None if loose == 0 else 'vector'
```

### Step 4: Assign unknown = bias_params_free

```python
evoked, fwd, noise_cov, _, _ = bias_params_free
```

### Step 5: Assign inv = make_inverse_operator(...)

```python
inv = make_inverse_operator(evoked.info, fwd, noise_cov, loose=loose, depth=None, verbose='debug')
```

### Step 6: Assign stc_mne = apply_inverse(...)

```python
stc_mne = apply_inverse(evoked, inv, lambda2, 'MNE', pick_ori=pick_ori, verbose='debug')
```

### Step 7: Assign atol = value

```python
atol = np.mean(np.abs(stc_mne.data)) * 1e-06
```

**Verification:**
```python
assert 3e-09 < atol < 3e-06
```

### Step 8: Call assert_allclose()

```python
assert_allclose(stc_mne.data, stc_e.data, atol=atol, rtol=0.0001)
```

### Step 9: Assign stc_e = apply_inverse(...)

```python
stc_e = apply_inverse(evoked, inv, lambda2, 'eLORETA', method_params=method_params, pick_ori=pick_ori, verbose='debug')
```


## Complete Example

```python
# Setup
# Fixtures: bias_params_free, loose, lambda2

# Workflow
'Test that eLORETA with no iterations is the same as MNE.'
method_params = dict(max_iter=0, force_equal=False)
pick_ori = None if loose == 0 else 'vector'
evoked, fwd, noise_cov, _, _ = bias_params_free
inv = make_inverse_operator(evoked.info, fwd, noise_cov, loose=loose, depth=None, verbose='debug')
stc_mne = apply_inverse(evoked, inv, lambda2, 'MNE', pick_ori=pick_ori, verbose='debug')
with pytest.warns(RuntimeWarning, match='converge'):
    stc_e = apply_inverse(evoked, inv, lambda2, 'eLORETA', method_params=method_params, pick_ori=pick_ori, verbose='debug')
atol = np.mean(np.abs(stc_mne.data)) * 1e-06
assert 3e-09 < atol < 3e-06
assert_allclose(stc_mne.data, stc_e.data, atol=atol, rtol=0.0001)
```

## Next Steps


---

*Source: test_inverse.py:607 | Complexity: Advanced | Last updated: 2026-05-18*