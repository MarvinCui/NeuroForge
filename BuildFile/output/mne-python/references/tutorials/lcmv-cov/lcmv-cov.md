# How To: Lcmv Cov

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test LCMV source power computation.

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
# Fixtures: weight_norm, pick_ori
```

## Step-by-Step Guide

### Step 1: 'Test LCMV source power computation.'

```python
'Test LCMV source power computation.'
```

**Verification:**
```python
assert this_evoked.ch_names == this_cov['names']
```

### Step 2: Assign unknown = _get_data(...)

```python
raw, epochs, evoked, data_cov, noise_cov, label, forward, forward_surf_ori, forward_fixed, forward_vol = _get_data()
```

**Verification:**
```python
assert stc.data.min() > 0
```

### Step 3: Call convert_forward_solution()

```python
convert_forward_solution(forward, surf_ori=True, copy=False)
```

**Verification:**
```python
assert stc.shape == (498, 1)
```

### Step 4: Assign filters = make_lcmv(...)

```python
filters = make_lcmv(evoked.info, forward, data_cov, noise_cov=noise_cov, weight_norm=weight_norm, pick_ori=pick_ori)
```

**Verification:**
```python
assert stc_1.data.min() < 0
```

### Step 5: Assign this_cov = pick_channels_cov(...)

```python
this_cov = pick_channels_cov(cov, evoked.ch_names, ordered=False)
```

**Verification:**
```python
assert stc_2.data.shape == (498, 498)
```

### Step 6: Assign this_evoked = evoked.copy.pick(...)

```python
this_evoked = evoked.copy().pick(this_cov['names'])
```

**Verification:**
```python
assert data.min() > 0
```

### Step 7: Assign unknown = value

```python
this_cov['projs'] = this_evoked.info['projs']
```

**Verification:**
```python
assert_allclose(data, stc.data, rtol=1e-12)
```

### Step 8: Assign stc = apply_lcmv_cov(...)

```python
stc = apply_lcmv_cov(this_cov, filters)
```

**Verification:**
```python
assert stc.data.min() > 0
```

### Step 9: Assign ev = EvokedArray(...)

```python
ev = EvokedArray(this_cov.data, this_evoked.info)
```

### Step 10: Assign stc_1 = apply_lcmv(...)

```python
stc_1 = apply_lcmv(ev, filters)
```

**Verification:**
```python
assert stc_1.data.min() < 0
```

### Step 11: Assign ev = EvokedArray(...)

```python
ev = EvokedArray(stc_1.data.T, this_evoked.info)
```

### Step 12: Assign stc_2 = apply_lcmv(...)

```python
stc_2 = apply_lcmv(ev, filters)
```

**Verification:**
```python
assert stc_2.data.shape == (498, 498)
```

### Step 13: Assign data = value

```python
data = np.diag(stc_2.data)[:, np.newaxis]
```

**Verification:**
```python
assert data.min() > 0
```

### Step 14: Call assert_allclose()

```python
assert_allclose(data, stc.data, rtol=1e-12)
```


## Complete Example

```python
# Setup
# Fixtures: weight_norm, pick_ori

# Workflow
'Test LCMV source power computation.'
raw, epochs, evoked, data_cov, noise_cov, label, forward, forward_surf_ori, forward_fixed, forward_vol = _get_data()
convert_forward_solution(forward, surf_ori=True, copy=False)
filters = make_lcmv(evoked.info, forward, data_cov, noise_cov=noise_cov, weight_norm=weight_norm, pick_ori=pick_ori)
for cov in (data_cov, noise_cov):
    this_cov = pick_channels_cov(cov, evoked.ch_names, ordered=False)
    this_evoked = evoked.copy().pick(this_cov['names'])
    this_cov['projs'] = this_evoked.info['projs']
    assert this_evoked.ch_names == this_cov['names']
    stc = apply_lcmv_cov(this_cov, filters)
    assert stc.data.min() > 0
    assert stc.shape == (498, 1)
    ev = EvokedArray(this_cov.data, this_evoked.info)
    stc_1 = apply_lcmv(ev, filters)
    assert stc_1.data.min() < 0
    ev = EvokedArray(stc_1.data.T, this_evoked.info)
    stc_2 = apply_lcmv(ev, filters)
    assert stc_2.data.shape == (498, 498)
    data = np.diag(stc_2.data)[:, np.newaxis]
    assert data.min() > 0
    assert_allclose(data, stc.data, rtol=1e-12)
```

## Next Steps


---

*Source: test_lcmv.py:650 | Complexity: Advanced | Last updated: 2026-05-18*