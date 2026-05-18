# How To: Min Distance Fit Dipole

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test dipole min_dist to inner_skull.

## Prerequisites

**Required Modules:**
- `os`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.datasets`
- `mne.dipole`
- `mne.io`
- `mne.proj`
- `mne.simulation`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test dipole min_dist to inner_skull.'

```python
'Test dipole min_dist to inner_skull.'
```

**Verification:**
```python
assert isinstance(residual, Evoked)
```

### Step 2: Assign subject = 'sample'

```python
subject = 'sample'
```

**Verification:**
```python
assert min_dist - 0.1 < dist[0] * 1000.0 < min_dist + 1.0
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw, preload=True)
```

### Step 4: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=False, eeg=True, exclude='bads')
```

### Step 5: Assign info = pick_info(...)

```python
info = pick_info(raw.info, picks)
```

### Step 6: Assign cov = read_cov(...)

```python
cov = read_cov(fname_cov)
```

### Step 7: Assign unknown = np.eye(...)

```python
cov['data'] = np.eye(cov['data'].shape[0])
```

### Step 8: Assign simulated_scalp_map = np.zeros(...)

```python
simulated_scalp_map = np.zeros(picks.shape[0])
```

### Step 9: Assign unknown = 1

```python
simulated_scalp_map[27:34] = 1
```

### Step 10: Assign simulated_scalp_map = value

```python
simulated_scalp_map = simulated_scalp_map[:, None]
```

### Step 11: Assign evoked = EvokedArray(...)

```python
evoked = EvokedArray(simulated_scalp_map, info, tmin=0)
```

### Step 12: Assign min_dist = 5.0

```python
min_dist = 5.0
```

### Step 13: Assign bem = read_bem_solution(...)

```python
bem = read_bem_solution(fname_bem)
```

### Step 14: Assign unknown = fit_dipole(...)

```python
dip, residual = fit_dipole(evoked, cov, bem, fname_trans, min_dist=min_dist, tol=0.0001)
```

**Verification:**
```python
assert isinstance(residual, Evoked)
```

### Step 15: Assign dist = _compute_depth(...)

```python
dist = _compute_depth(dip, fname_bem, fname_trans, subject, subjects_dir)
```

**Verification:**
```python
assert min_dist - 0.1 < dist[0] * 1000.0 < min_dist + 1.0
```

### Step 16: Call fit_dipole()

```python
fit_dipole(evoked, cov, fname_bem, fname_trans, -1.0)
```

### Step 17: Call fit_dipole()

```python
fit_dipole(evoked, cov, bem, trans=None)
```


## Complete Example

```python
# Workflow
'Test dipole min_dist to inner_skull.'
subject = 'sample'
raw = read_raw_fif(fname_raw, preload=True)
picks = pick_types(raw.info, meg=False, eeg=True, exclude='bads')
info = pick_info(raw.info, picks)
cov = read_cov(fname_cov)
cov['data'] = np.eye(cov['data'].shape[0])
simulated_scalp_map = np.zeros(picks.shape[0])
simulated_scalp_map[27:34] = 1
simulated_scalp_map = simulated_scalp_map[:, None]
evoked = EvokedArray(simulated_scalp_map, info, tmin=0)
min_dist = 5.0
bem = read_bem_solution(fname_bem)
dip, residual = fit_dipole(evoked, cov, bem, fname_trans, min_dist=min_dist, tol=0.0001)
assert isinstance(residual, Evoked)
dist = _compute_depth(dip, fname_bem, fname_trans, subject, subjects_dir)
assert min_dist - 0.1 < dist[0] * 1000.0 < min_dist + 1.0
with pytest.raises(ValueError, match='min_dist should be positive'):
    fit_dipole(evoked, cov, fname_bem, fname_trans, -1.0)
with pytest.raises(ValueError, match='not spherical'):
    fit_dipole(evoked, cov, bem, trans=None)
```

## Next Steps


---

*Source: test_dipole.py:332 | Complexity: Advanced | Last updated: 2026-05-18*