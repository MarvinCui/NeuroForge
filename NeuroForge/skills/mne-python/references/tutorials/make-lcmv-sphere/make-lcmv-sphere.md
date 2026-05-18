# How To: Make Lcmv Sphere

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test LCMV with sphere head model.

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
# Fixtures: pick_ori, weight_norm, evoked_fwd_noise_data
```

## Step-by-Step Guide

### Step 1: 'Test LCMV with sphere head model.'

```python
'Test LCMV with sphere head model.'
```

**Verification:**
```python
assert isinstance(stc_sphere, VolSourceEstimate)
```

### Step 2: Assign unknown = evoked_fwd_noise_data

```python
evoked, fwd_sphere, noise_cov, data_cov = evoked_fwd_noise_data
```

**Verification:**
```python
assert 0.08 < tmax < 0.15, tmax
```

### Step 3: Assign filters = make_lcmv(...)

```python
filters = make_lcmv(evoked.info, fwd_sphere, data_cov, reg=0.1, noise_cov=noise_cov, weight_norm=weight_norm, pick_ori=pick_ori, reduce_rank=True)
```

**Verification:**
```python
assert min_ < np.max(max_stc) < max_, (min_, np.max(max_stc), max_)
```

### Step 4: Assign stc_sphere = apply_lcmv(...)

```python
stc_sphere = apply_lcmv(evoked, filters)
```

**Verification:**
```python
assert isinstance(stc_sphere, VolSourceEstimate)
```

### Step 5: Call stc_sphere.crop()

```python
stc_sphere.crop(0.02, None)
```

### Step 6: Assign stc_pow = np.sum(...)

```python
stc_pow = np.sum(stc_sphere.data, axis=1)
```

### Step 7: Assign idx = np.argmax(...)

```python
idx = np.argmax(stc_pow)
```

### Step 8: Assign max_stc = value

```python
max_stc = stc_sphere.data[idx]
```

### Step 9: Assign tmax = value

```python
tmax = stc_sphere.times[np.argmax(max_stc)]
```

**Verification:**
```python
assert 0.08 < tmax < 0.15, tmax
```

### Step 10: Assign unknown = value

```python
min_, max_ = (1.0, 4.5)
```

**Verification:**
```python
assert min_ < np.max(max_stc) < max_, (min_, np.max(max_stc), max_)
```

### Step 11: Call make_lcmv()

```python
make_lcmv(evoked.info, fwd_sphere, data_cov, reg=0.1, noise_cov=noise_cov, weight_norm=weight_norm, pick_ori=pick_ori, reduce_rank=False, rank='full')
```

### Step 12: Assign stc_sphere = stc_sphere.magnitude(...)

```python
stc_sphere = stc_sphere.magnitude()
```

### Step 13: Assign stc_sphere = abs(...)

```python
stc_sphere = abs(stc_sphere)
```


## Complete Example

```python
# Setup
# Fixtures: pick_ori, weight_norm, evoked_fwd_noise_data

# Workflow
'Test LCMV with sphere head model.'
evoked, fwd_sphere, noise_cov, data_cov = evoked_fwd_noise_data
with pytest.raises(ValueError, match='Singular matrix detected'), _record_warnings(), pytest.warns(RuntimeWarning, match='(positive semidefinite|largest eigenvalu)'):
    make_lcmv(evoked.info, fwd_sphere, data_cov, reg=0.1, noise_cov=noise_cov, weight_norm=weight_norm, pick_ori=pick_ori, reduce_rank=False, rank='full')
filters = make_lcmv(evoked.info, fwd_sphere, data_cov, reg=0.1, noise_cov=noise_cov, weight_norm=weight_norm, pick_ori=pick_ori, reduce_rank=True)
stc_sphere = apply_lcmv(evoked, filters)
if isinstance(stc_sphere, VolVectorSourceEstimate):
    stc_sphere = stc_sphere.magnitude()
else:
    stc_sphere = abs(stc_sphere)
assert isinstance(stc_sphere, VolSourceEstimate)
stc_sphere.crop(0.02, None)
stc_pow = np.sum(stc_sphere.data, axis=1)
idx = np.argmax(stc_pow)
max_stc = stc_sphere.data[idx]
tmax = stc_sphere.times[np.argmax(max_stc)]
assert 0.08 < tmax < 0.15, tmax
min_, max_ = (1.0, 4.5)
if weight_norm is None:
    min_ *= 2e-07
    max_ *= 2e-07
assert min_ < np.max(max_stc) < max_, (min_, np.max(max_stc), max_)
```

## Next Steps


---

*Source: test_lcmv.py:593 | Complexity: Advanced | Last updated: 2026-05-18*