# How To: Localization Bias Free

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test localization bias for free-orientation DICS.

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
# Fixtures: bias_params_free, reg, pick_ori, weight_norm, use_cov, depth, lower, upper, real_filter
```

## Step-by-Step Guide

### Step 1: 'Test localization bias for free-orientation DICS.'

```python
'Test localization bias for free-orientation DICS.'
```

**Verification:**
```python
assert lower <= perc <= upper
```

### Step 2: Assign unknown = bias_params_free

```python
evoked, fwd, noise_cov, data_cov, want = bias_params_free
```

### Step 3: Assign noise_csd = _cov_as_csd(...)

```python
noise_csd = _cov_as_csd(noise_cov, evoked.info)
```

### Step 4: Assign data_csd = _cov_as_csd(...)

```python
data_csd = _cov_as_csd(data_cov, evoked.info)
```

### Step 5: Assign filters = make_dics(...)

```python
filters = make_dics(evoked.info, fwd, data_csd, reg, noise_csd, pick_ori=pick_ori, weight_norm=weight_norm, depth=depth, real_filter=real_filter)
```

### Step 6: Assign loc = value

```python
loc = apply_dics(evoked, filters).data
```

### Step 7: Assign loc = value

```python
loc = np.linalg.norm(loc, axis=1) if pick_ori == 'vector' else np.abs(loc)
```

### Step 8: Assign perc = value

```python
perc = (want == np.argmax(loc, axis=0)).mean() * 100
```

**Verification:**
```python
assert lower <= perc <= upper
```

### Step 9: Call evoked.pick()

```python
evoked.pick(picks='grad')
```

### Step 10: Assign noise_csd = None

```python
noise_csd = None
```


## Complete Example

```python
# Setup
# Fixtures: bias_params_free, reg, pick_ori, weight_norm, use_cov, depth, lower, upper, real_filter

# Workflow
'Test localization bias for free-orientation DICS.'
evoked, fwd, noise_cov, data_cov, want = bias_params_free
noise_csd = _cov_as_csd(noise_cov, evoked.info)
data_csd = _cov_as_csd(data_cov, evoked.info)
del noise_cov, data_cov
if not use_cov:
    evoked.pick(picks='grad')
    noise_csd = None
filters = make_dics(evoked.info, fwd, data_csd, reg, noise_csd, pick_ori=pick_ori, weight_norm=weight_norm, depth=depth, real_filter=real_filter)
loc = apply_dics(evoked, filters).data
loc = np.linalg.norm(loc, axis=1) if pick_ori == 'vector' else np.abs(loc)
perc = (want == np.argmax(loc, axis=0)).mean() * 100
assert lower <= perc <= upper
```

## Next Steps


---

*Source: test_dics.py:817 | Complexity: Advanced | Last updated: 2026-05-18*