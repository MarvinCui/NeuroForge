# How To: Rap Music Sphere

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test RAP-MUSIC with real data, sphere model, MEG only.

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

### Step 1: 'Test RAP-MUSIC with real data, sphere model, MEG only.'

```python
'Test RAP-MUSIC with real data, sphere model, MEG only.'
```

**Verification:**
```python
assert_var_exp_log(log.getvalue(), 47, 49)
```

### Step 2: Assign unknown = _get_data(...)

```python
evoked, noise_cov = _get_data(ch_decim=8)
```

**Verification:**
```python
assert pos.shape == (2, 3)
```

### Step 3: Assign sphere = mne.make_sphere_model(...)

```python
sphere = mne.make_sphere_model(r0=(0.0, 0.0, 0.04))
```

**Verification:**
```python
assert (pos[:, 0] < 0).sum() == 1
```

### Step 4: Assign src = mne.setup_volume_source_space(...)

```python
src = mne.setup_volume_source_space(subject=None, pos=10.0, sphere=(0.0, 0.0, 40, 65.0), mindist=5.0, exclude=0.0, sphere_units='mm')
```

**Verification:**
```python
assert (pos[:, 0] > 0).sum() == 1
```

### Step 5: Assign forward = mne.make_forward_solution(...)

```python
forward = mne.make_forward_solution(evoked.info, trans=None, src=src, bem=sphere)
```

**Verification:**
```python
assert 1e-10 < dipoles[0].amplitude[0] < 1e-07
```

### Step 6: Call assert_var_exp_log()

```python
assert_var_exp_log(log.getvalue(), 47, 49)
```

**Verification:**
```python
assert np.max(np.abs(np.dot(dip_fit.ori, dipoles[0].ori[0]))) > 0.99
```

### Step 7: Assign pos = np.array(...)

```python
pos = np.array([dip.pos[0] for dip in dipoles])
```

**Verification:**
```python
assert np.max(np.abs(np.dot(dip_fit.ori, dipoles[1].ori[0]))) > 0.99
```

### Step 8: Assign dip_fit = value

```python
dip_fit = mne.fit_dipole(evoked, noise_cov, sphere)[0]
```

**Verification:**
```python
assert 0.004 <= dist < 0.007
```

### Step 9: Assign idx = dip_fit.gof.argmax(...)

```python
idx = dip_fit.gof.argmax()
```

**Verification:**
```python
assert_allclose(dipoles[0].gof[idx], dip_fit.gof[idx], atol=3)
```

### Step 10: Assign dist = np.linalg.norm(...)

```python
dist = np.linalg.norm(dipoles[0].pos[idx] - dip_fit.pos[idx])
```

**Verification:**
```python
assert 0.004 <= dist < 0.007
```

### Step 11: Call assert_allclose()

```python
assert_allclose(dipoles[0].gof[idx], dip_fit.gof[idx], atol=3)
```

### Step 12: Assign dipoles = rap_music(...)

```python
dipoles = rap_music(evoked, forward, noise_cov, n_dipoles=2, verbose=True)
```


## Complete Example

```python
# Workflow
'Test RAP-MUSIC with real data, sphere model, MEG only.'
evoked, noise_cov = _get_data(ch_decim=8)
sphere = mne.make_sphere_model(r0=(0.0, 0.0, 0.04))
src = mne.setup_volume_source_space(subject=None, pos=10.0, sphere=(0.0, 0.0, 40, 65.0), mindist=5.0, exclude=0.0, sphere_units='mm')
forward = mne.make_forward_solution(evoked.info, trans=None, src=src, bem=sphere)
with catch_logging() as log:
    dipoles = rap_music(evoked, forward, noise_cov, n_dipoles=2, verbose=True)
assert_var_exp_log(log.getvalue(), 47, 49)
pos = np.array([dip.pos[0] for dip in dipoles])
assert pos.shape == (2, 3)
assert (pos[:, 0] < 0).sum() == 1
assert (pos[:, 0] > 0).sum() == 1
assert 1e-10 < dipoles[0].amplitude[0] < 1e-07
dip_fit = mne.fit_dipole(evoked, noise_cov, sphere)[0]
assert np.max(np.abs(np.dot(dip_fit.ori, dipoles[0].ori[0]))) > 0.99
assert np.max(np.abs(np.dot(dip_fit.ori, dipoles[1].ori[0]))) > 0.99
idx = dip_fit.gof.argmax()
dist = np.linalg.norm(dipoles[0].pos[idx] - dip_fit.pos[idx])
assert 0.004 <= dist < 0.007
assert_allclose(dipoles[0].gof[idx], dip_fit.gof[idx], atol=3)
```

## Next Steps


---

*Source: test_rap_music.py:167 | Complexity: Advanced | Last updated: 2026-05-18*