# How To: Orientation Max Power

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test orientation selection for bias for max-power DICS.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.beamformer`
- `mne.beamformer._compute_beamformer`
- `mne.beamformer._dics`
- `mne.beamformer.tests.test_lcmv`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.proj`
- `mne.surface`
- `mne.time_frequency`
- `mne.time_frequency.csd`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: bias_params_fixed, bias_params_free, weight_norm, lower, upper, lower_ori, upper_ori, real_filter
```

## Step-by-Step Guide

### Step 1: 'Test orientation selection for bias for max-power DICS.'

```python
'Test orientation selection for bias for max-power DICS.'
```

**Verification:**
```python
assert ori.shape == (246, 3)
```

### Step 2: Assign unknown = bias_params_fixed

```python
evoked, _, noise_cov, data_cov, want = bias_params_fixed
```

**Verification:**
```python
assert lower <= perc <= upper
```

### Step 3: Assign noise_csd = _cov_as_csd(...)

```python
noise_csd = _cov_as_csd(noise_cov, evoked.info)
```

**Verification:**
```python
assert fwd['coord_frame'] == FIFF.FIFFV_COORD_HEAD
```

### Step 4: Assign data_csd = _cov_as_csd(...)

```python
data_csd = _cov_as_csd(data_cov, evoked.info)
```

**Verification:**
```python
assert_allclose(np.linalg.norm(nn, axis=1), 1, atol=1e-06)
```

### Step 5: Assign fwd = value

```python
fwd = bias_params_free[1]
```

**Verification:**
```python
assert_allclose(np.linalg.norm(ori, axis=1), 1, atol=1e-12)
```

### Step 6: Assign filters = make_dics(...)

```python
filters = make_dics(evoked.info, fwd, data_csd, 0.05, noise_csd, pick_ori='max-power', weight_norm=weight_norm, depth=None, real_filter=real_filter)
```

**Verification:**
```python
assert_array_less(dots, 1)
```

### Step 7: Assign loc = np.abs(...)

```python
loc = np.abs(apply_dics(evoked, filters).data)
```

**Verification:**
```python
assert_array_less(0, dots)
```

### Step 8: Assign ori = value

```python
ori = filters['max_power_ori'][0]
```

**Verification:**
```python
assert lower_ori < got < upper_ori
```

### Step 9: Assign loc = np.abs(...)

```python
loc = np.abs(loc)
```

### Step 10: Assign max_idx = np.argmax(...)

```python
max_idx = np.argmax(loc, axis=0)
```

### Step 11: Assign mask = value

```python
mask = want == max_idx
```

### Step 12: Assign perc = value

```python
perc = mask.mean() * 100
```

**Verification:**
```python
assert lower <= perc <= upper
```

### Step 13: Assign nn = np.concatenate(...)

```python
nn = np.concatenate([s['nn'][v] for s, v in zip(fwd['src'], filters['vertices'])])
```

### Step 14: Assign nn = value

```python
nn = nn[want]
```

### Step 15: Assign nn = apply_trans(...)

```python
nn = apply_trans(invert_transform(fwd['mri_head_t']), nn, move=False)
```

### Step 16: Call assert_allclose()

```python
assert_allclose(np.linalg.norm(nn, axis=1), 1, atol=1e-06)
```

### Step 17: Call assert_allclose()

```python
assert_allclose(np.linalg.norm(ori, axis=1), 1, atol=1e-12)
```

### Step 18: Assign dots = np.abs(...)

```python
dots = np.abs((nn[mask] * ori[mask]).sum(-1))
```

### Step 19: Call assert_array_less()

```python
assert_array_less(dots, 1)
```

### Step 20: Call assert_array_less()

```python
assert_array_less(0, dots)
```

### Step 21: Assign got = np.mean(...)

```python
got = np.mean(dots)
```

**Verification:**
```python
assert lower_ori < got < upper_ori
```


## Complete Example

```python
# Setup
# Fixtures: bias_params_fixed, bias_params_free, weight_norm, lower, upper, lower_ori, upper_ori, real_filter

# Workflow
'Test orientation selection for bias for max-power DICS.'
evoked, _, noise_cov, data_cov, want = bias_params_fixed
noise_csd = _cov_as_csd(noise_cov, evoked.info)
data_csd = _cov_as_csd(data_cov, evoked.info)
del data_cov, noise_cov
fwd = bias_params_free[1]
filters = make_dics(evoked.info, fwd, data_csd, 0.05, noise_csd, pick_ori='max-power', weight_norm=weight_norm, depth=None, real_filter=real_filter)
loc = np.abs(apply_dics(evoked, filters).data)
ori = filters['max_power_ori'][0]
assert ori.shape == (246, 3)
loc = np.abs(loc)
max_idx = np.argmax(loc, axis=0)
mask = want == max_idx
perc = mask.mean() * 100
assert lower <= perc <= upper
assert fwd['coord_frame'] == FIFF.FIFFV_COORD_HEAD
nn = np.concatenate([s['nn'][v] for s, v in zip(fwd['src'], filters['vertices'])])
nn = nn[want]
nn = apply_trans(invert_transform(fwd['mri_head_t']), nn, move=False)
assert_allclose(np.linalg.norm(nn, axis=1), 1, atol=1e-06)
assert_allclose(np.linalg.norm(ori, axis=1), 1, atol=1e-12)
dots = np.abs((nn[mask] * ori[mask]).sum(-1))
assert_array_less(dots, 1)
assert_array_less(0, dots)
got = np.mean(dots)
assert lower_ori < got < upper_ori
```

## Next Steps


---

*Source: test_dics.py:864 | Complexity: Advanced | Last updated: 2026-05-18*