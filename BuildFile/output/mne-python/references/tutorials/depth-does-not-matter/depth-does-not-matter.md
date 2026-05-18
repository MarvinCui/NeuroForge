# How To: Depth Does Not Matter

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that depth weighting does not matter for normalized filters.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `contextlib`
- `copy`
- `inspect`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `scipy.spatial.distance`
- `mne`
- `mne`
- `mne._fiff.compensator`
- `mne._fiff.constants`
- `mne.beamformer`
- `mne.beamformer._compute_beamformer`
- `mne.datasets`
- `mne.fixes`
- `mne.minimum_norm`
- `mne.minimum_norm.tests.test_inverse`
- `mne.simulation`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: bias_params_free, weight_norm, pick_ori
```

## Step-by-Step Guide

### Step 1: 'Test that depth weighting does not matter for normalized filters.'

```python
'Test that depth weighting does not matter for normalized filters.'
```

**Verification:**
```python
assert data.shape == data_depth.shape
```

### Step 2: Assign unknown = bias_params_free

```python
evoked, fwd, noise_cov, data_cov, _ = bias_params_free
```

**Verification:**
```python
assert_allclose(d1, d2, atol=atol)
```

### Step 3: Assign data = value

```python
data = apply_lcmv(evoked, make_lcmv(evoked.info, fwd, data_cov, 0.05, noise_cov, pick_ori=pick_ori, weight_norm=weight_norm, depth=0.0)).data
```

### Step 4: Assign data_depth = value

```python
data_depth = apply_lcmv(evoked, make_lcmv(evoked.info, fwd, data_cov, 0.05, noise_cov, pick_ori=pick_ori, weight_norm=weight_norm, depth=1.0)).data
```

**Verification:**
```python
assert data.shape == data_depth.shape
```

### Step 5: Assign atol = value

```python
atol = np.linalg.norm(d1) * 1e-07
```

### Step 6: Call assert_allclose()

```python
assert_allclose(d1, d2, atol=atol)
```


## Complete Example

```python
# Setup
# Fixtures: bias_params_free, weight_norm, pick_ori

# Workflow
'Test that depth weighting does not matter for normalized filters.'
evoked, fwd, noise_cov, data_cov, _ = bias_params_free
data = apply_lcmv(evoked, make_lcmv(evoked.info, fwd, data_cov, 0.05, noise_cov, pick_ori=pick_ori, weight_norm=weight_norm, depth=0.0)).data
data_depth = apply_lcmv(evoked, make_lcmv(evoked.info, fwd, data_cov, 0.05, noise_cov, pick_ori=pick_ori, weight_norm=weight_norm, depth=1.0)).data
assert data.shape == data_depth.shape
for d1, d2 in zip(data, data_depth):
    d2 *= np.sign(np.dot(d1.ravel(), d2.ravel()))
    atol = np.linalg.norm(d1) * 1e-07
    assert_allclose(d1, d2, atol=atol)
```

## Next Steps


---

*Source: test_lcmv.py:1061 | Complexity: Intermediate | Last updated: 2026-05-18*