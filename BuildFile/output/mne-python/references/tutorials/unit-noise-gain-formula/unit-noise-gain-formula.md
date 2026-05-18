# How To: Unit Noise Gain Formula

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test unit-noise-gain filter against formula.

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
# Fixtures: pick_ori, weight_norm, reg, inversion
```

## Step-by-Step Guide

### Step 1: 'Test unit-noise-gain filter against formula.'

```python
'Test unit-noise-gain filter against formula.'
```

**Verification:**
```python
assert len(raw.ch_names) == 102
```

### Step 2: Assign raw = mne.io.read_raw_fif(...)

```python
raw = mne.io.read_raw_fif(fname_raw, preload=True)
```

### Step 3: Assign events = mne.find_events(...)

```python
events = mne.find_events(raw)
```

### Step 4: Call raw.pick()

```python
raw.pick(picks='mag')
```

**Verification:**
```python
assert len(raw.ch_names) == 102
```

### Step 5: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, None, preload=True)
```

### Step 6: Assign data_cov = mne.compute_covariance(...)

```python
data_cov = mne.compute_covariance(epochs, tmin=0.04, tmax=0.15)
```

### Step 7: Assign noise_cov = mne.make_ad_hoc_cov(...)

```python
noise_cov = mne.make_ad_hoc_cov(epochs.info, std=dict(grad=1.0, mag=1.0))
```

### Step 8: Assign forward = mne.read_forward_solution(...)

```python
forward = mne.read_forward_solution(fname_fwd)
```

### Step 9: Call convert_forward_solution()

```python
convert_forward_solution(forward, surf_ori=True, copy=False)
```

### Step 10: Assign rank = None

```python
rank = None
```

### Step 11: Assign kwargs = dict(...)

```python
kwargs = dict(reg=reg, noise_cov=noise_cov, pick_ori=pick_ori, weight_norm=weight_norm, rank=rank, inversion=inversion)
```

### Step 12: Assign filters = make_lcmv(...)

```python
filters = make_lcmv(epochs.info, forward, data_cov, **kwargs)
```

### Step 13: Assign unknown = _prepare_beamformer_input(...)

```python
_, _, _, _, G, _, _, _ = _prepare_beamformer_input(epochs.info, forward, None, 'vector', noise_cov=noise_cov, rank=rank, pca=False, exp=None)
```

### Step 14: Assign unknown = value

```python
n_channels, n_sources = G.shape
```

### Step 15: Assign G = _reshape_view(...)

```python
G = _reshape_view(G, (n_channels, n_sources, 3))
```

### Step 16: Assign G = G.transpose(...)

```python
G = G.transpose(1, 2, 0)
```

### Step 17: Call _assert_weight_norm()

```python
_assert_weight_norm(filters, G)
```

### Step 18: Call make_lcmv()

```python
make_lcmv(epochs.info, forward, data_cov, **kwargs)
```


## Complete Example

```python
# Setup
# Fixtures: pick_ori, weight_norm, reg, inversion

# Workflow
'Test unit-noise-gain filter against formula.'
raw = mne.io.read_raw_fif(fname_raw, preload=True)
events = mne.find_events(raw)
raw.pick(picks='mag')
assert len(raw.ch_names) == 102
epochs = mne.Epochs(raw, events, None, preload=True)
data_cov = mne.compute_covariance(epochs, tmin=0.04, tmax=0.15)
noise_cov = mne.make_ad_hoc_cov(epochs.info, std=dict(grad=1.0, mag=1.0))
forward = mne.read_forward_solution(fname_fwd)
convert_forward_solution(forward, surf_ori=True, copy=False)
rank = None
kwargs = dict(reg=reg, noise_cov=noise_cov, pick_ori=pick_ori, weight_norm=weight_norm, rank=rank, inversion=inversion)
if inversion == 'single' and pick_ori == 'vector' and (weight_norm == 'unit-noise-gain-invariant'):
    with pytest.raises(ValueError, match='Cannot use'):
        make_lcmv(epochs.info, forward, data_cov, **kwargs)
    return
filters = make_lcmv(epochs.info, forward, data_cov, **kwargs)
_, _, _, _, G, _, _, _ = _prepare_beamformer_input(epochs.info, forward, None, 'vector', noise_cov=noise_cov, rank=rank, pca=False, exp=None)
n_channels, n_sources = G.shape
n_sources //= 3
G = _reshape_view(G, (n_channels, n_sources, 3))
G = G.transpose(1, 2, 0)
_assert_weight_norm(filters, G)
```

## Next Steps


---

*Source: test_lcmv.py:1153 | Complexity: Advanced | Last updated: 2026-05-18*