# How To: Rap Music Simulated

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test RAP-MUSIC with simulated evoked.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.beamformer`
- `mne.cov`
- `mne.datasets`
- `mne.minimum_norm.tests.test_inverse`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test RAP-MUSIC with simulated evoked.'

```python
'Test RAP-MUSIC with simulated evoked.'
```

**Verification:**
```python
assert_var_exp_log(log.getvalue(), 89, 91)
```

### Step 2: Assign unknown = _get_data(...)

```python
evoked, noise_cov = _get_data(ch_decim=16)
```

**Verification:**
```python
assert 97 < dipoles[0].gof.max() < 100
```

### Step 3: Assign forward = mne.read_forward_solution(...)

```python
forward = mne.read_forward_solution(fname_fwd)
```

**Verification:**
```python
assert 91 < dipoles[1].gof.max() < 93
```

### Step 4: Assign forward = mne.pick_channels_forward(...)

```python
forward = mne.pick_channels_forward(forward, evoked.ch_names)
```

**Verification:**
```python
assert dipoles[0].gof.min() >= 0.0
```

### Step 5: Assign forward_surf_ori = mne.convert_forward_solution(...)

```python
forward_surf_ori = mne.convert_forward_solution(forward, surf_ori=True)
```

### Step 6: Assign forward_fixed = mne.convert_forward_solution(...)

```python
forward_fixed = mne.convert_forward_solution(forward, force_fixed=True, surf_ori=True, use_cps=True)
```

### Step 7: Assign n_dipoles = 2

```python
n_dipoles = 2
```

### Step 8: Assign unknown = simu_data(...)

```python
sim_evoked, stc = simu_data(evoked, forward_fixed, noise_cov, n_dipoles, evoked.times, nave=evoked.nave)
```

### Step 9: Call assert_var_exp_log()

```python
assert_var_exp_log(log.getvalue(), 89, 91)
```

### Step 10: Call _check_dipoles()

```python
_check_dipoles(dipoles, forward_fixed, stc, sim_evoked)
```

**Verification:**
```python
assert 97 < dipoles[0].gof.max() < 100
```

### Step 11: Assign nave = 100000

```python
nave = 100000
```

### Step 12: Assign unknown = simu_data(...)

```python
sim_evoked, stc = simu_data(evoked, forward_fixed, noise_cov, n_dipoles, evoked.times, nave=nave)
```

### Step 13: Assign unknown = rap_music(...)

```python
dipoles, residual = rap_music(sim_evoked, forward_fixed, noise_cov, n_dipoles=n_dipoles, return_residual=True)
```

### Step 14: Call _check_dipoles()

```python
_check_dipoles(dipoles, forward_fixed, stc, sim_evoked, residual)
```

### Step 15: Assign unknown = rap_music(...)

```python
dipoles, residual = rap_music(sim_evoked, forward, noise_cov, n_dipoles=n_dipoles, return_residual=True)
```

### Step 16: Call _check_dipoles()

```python
_check_dipoles(dipoles, forward_fixed, stc, sim_evoked, residual)
```

### Step 17: Assign unknown = rap_music(...)

```python
dipoles, residual = rap_music(sim_evoked, forward_surf_ori, noise_cov, n_dipoles=n_dipoles, return_residual=True)
```

### Step 18: Call _check_dipoles()

```python
_check_dipoles(dipoles, forward_fixed, stc, sim_evoked, residual)
```

### Step 19: Assign dipoles = rap_music(...)

```python
dipoles = rap_music(sim_evoked, forward_fixed, noise_cov, n_dipoles=n_dipoles, verbose=True)
```


## Complete Example

```python
# Workflow
'Test RAP-MUSIC with simulated evoked.'
evoked, noise_cov = _get_data(ch_decim=16)
forward = mne.read_forward_solution(fname_fwd)
forward = mne.pick_channels_forward(forward, evoked.ch_names)
forward_surf_ori = mne.convert_forward_solution(forward, surf_ori=True)
forward_fixed = mne.convert_forward_solution(forward, force_fixed=True, surf_ori=True, use_cps=True)
n_dipoles = 2
sim_evoked, stc = simu_data(evoked, forward_fixed, noise_cov, n_dipoles, evoked.times, nave=evoked.nave)
with catch_logging() as log:
    dipoles = rap_music(sim_evoked, forward_fixed, noise_cov, n_dipoles=n_dipoles, verbose=True)
assert_var_exp_log(log.getvalue(), 89, 91)
_check_dipoles(dipoles, forward_fixed, stc, sim_evoked)
assert 97 < dipoles[0].gof.max() < 100
assert 91 < dipoles[1].gof.max() < 93
assert dipoles[0].gof.min() >= 0.0
nave = 100000
sim_evoked, stc = simu_data(evoked, forward_fixed, noise_cov, n_dipoles, evoked.times, nave=nave)
dipoles, residual = rap_music(sim_evoked, forward_fixed, noise_cov, n_dipoles=n_dipoles, return_residual=True)
_check_dipoles(dipoles, forward_fixed, stc, sim_evoked, residual)
dipoles, residual = rap_music(sim_evoked, forward, noise_cov, n_dipoles=n_dipoles, return_residual=True)
_check_dipoles(dipoles, forward_fixed, stc, sim_evoked, residual)
dipoles, residual = rap_music(sim_evoked, forward_surf_ori, noise_cov, n_dipoles=n_dipoles, return_residual=True)
_check_dipoles(dipoles, forward_fixed, stc, sim_evoked, residual)
```

## Next Steps


---

*Source: test_rap_music.py:114 | Complexity: Advanced | Last updated: 2026-05-18*