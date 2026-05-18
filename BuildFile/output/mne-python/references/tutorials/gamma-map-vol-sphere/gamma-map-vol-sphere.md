# How To: Gamma Map Vol Sphere

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Gamma MAP with a sphere forward and volumic source space.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne.cov`
- `mne.datasets`
- `mne.dipole`
- `mne.inverse_sparse`
- `mne.inverse_sparse.mxne_inverse`
- `mne.minimum_norm.tests.test_inverse`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Gamma MAP with a sphere forward and volumic source space.'

```python
'Gamma MAP with a sphere forward and volumic source space.'
```

**Verification:**
```python
assert_array_almost_equal(stc.times, evoked.times, 5)
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(fname_evoked, condition=0, baseline=(None, 0), proj=False)
```

**Verification:**
```python
assert_array_almost_equal(stc.times, evoked.times, 5)
```

### Step 3: Call evoked.resample()

```python
evoked.resample(50, npad=100)
```

**Verification:**
```python
assert dip_gmap[0].pos[0] in src[0]['rr'][stc.vertices[0]]
```

### Step 4: Call evoked.crop()

```python
evoked.crop(tmin=0.1, tmax=0.16)
```

**Verification:**
```python
assert np.abs(np.dot(dip_fit.ori[0], dip_gmap.ori[0])) > 0.99
```

### Step 5: Assign cov = read_cov(...)

```python
cov = read_cov(fname_cov)
```

### Step 6: Assign cov = regularize(...)

```python
cov = regularize(cov, evoked.info, rank=dict(eeg=58))
```

### Step 7: Assign info = value

```python
info = evoked.info
```

### Step 8: Assign sphere = mne.make_sphere_model(...)

```python
sphere = mne.make_sphere_model(r0=(0.0, 0.0, 0.0), head_radius=0.08)
```

### Step 9: Assign src = mne.setup_volume_source_space(...)

```python
src = mne.setup_volume_source_space(subject=None, pos=30.0, mri=None, sphere=(0.0, 0.0, 0.0, 0.08), bem=None, mindist=5.0, exclude=2.0, sphere_units='m')
```

### Step 10: Assign fwd = mne.make_forward_solution(...)

```python
fwd = mne.make_forward_solution(info, trans=None, src=src, bem=sphere, eeg=False, meg=True)
```

### Step 11: Assign alpha = 0.5

```python
alpha = 0.5
```

### Step 12: Assign stc = gamma_map(...)

```python
stc = gamma_map(evoked, fwd, cov, alpha, tol=0.0001, xyz_same_gamma=False, update_mode=2, return_residual=False)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(stc.times, evoked.times, 5)
```

### Step 14: Assign stc = gamma_map(...)

```python
stc = gamma_map(evoked, fwd, cov, alpha, loose=0.2, return_residual=False)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(stc.times, evoked.times, 5)
```

### Step 16: Assign stc = mne.VolSourceEstimate(...)

```python
stc = mne.VolSourceEstimate(5e-08 * np.random.RandomState(42).randn(1, 4), vertices=[stc.vertices[0][:1]], tmin=stc.tmin, tstep=stc.tstep)
```

### Step 17: Assign evoked_dip = mne.simulation.simulate_evoked(...)

```python
evoked_dip = mne.simulation.simulate_evoked(fwd, stc, info, cov, nave=1000000000.0, use_cps=True)
```

### Step 18: Assign dip_gmap = gamma_map(...)

```python
dip_gmap = gamma_map(evoked_dip, fwd, cov, 0.1, return_as_dipoles=True)
```

### Step 19: Assign amp_max = value

```python
amp_max = [np.max(d.amplitude) for d in dip_gmap]
```

### Step 20: Assign dip_gmap = value

```python
dip_gmap = dip_gmap[np.argmax(amp_max)]
```

**Verification:**
```python
assert dip_gmap[0].pos[0] in src[0]['rr'][stc.vertices[0]]
```

### Step 21: Assign dip_fit = value

```python
dip_fit = mne.fit_dipole(evoked_dip, cov, sphere)[0]
```

**Verification:**
```python
assert np.abs(np.dot(dip_fit.ori[0], dip_gmap.ori[0])) > 0.99
```


## Complete Example

```python
# Workflow
'Gamma MAP with a sphere forward and volumic source space.'
evoked = read_evokeds(fname_evoked, condition=0, baseline=(None, 0), proj=False)
evoked.resample(50, npad=100)
evoked.crop(tmin=0.1, tmax=0.16)
cov = read_cov(fname_cov)
cov = regularize(cov, evoked.info, rank=dict(eeg=58))
info = evoked.info
sphere = mne.make_sphere_model(r0=(0.0, 0.0, 0.0), head_radius=0.08)
src = mne.setup_volume_source_space(subject=None, pos=30.0, mri=None, sphere=(0.0, 0.0, 0.0, 0.08), bem=None, mindist=5.0, exclude=2.0, sphere_units='m')
fwd = mne.make_forward_solution(info, trans=None, src=src, bem=sphere, eeg=False, meg=True)
alpha = 0.5
stc = gamma_map(evoked, fwd, cov, alpha, tol=0.0001, xyz_same_gamma=False, update_mode=2, return_residual=False)
assert_array_almost_equal(stc.times, evoked.times, 5)
stc = gamma_map(evoked, fwd, cov, alpha, loose=0.2, return_residual=False)
assert_array_almost_equal(stc.times, evoked.times, 5)
stc = mne.VolSourceEstimate(5e-08 * np.random.RandomState(42).randn(1, 4), vertices=[stc.vertices[0][:1]], tmin=stc.tmin, tstep=stc.tstep)
evoked_dip = mne.simulation.simulate_evoked(fwd, stc, info, cov, nave=1000000000.0, use_cps=True)
dip_gmap = gamma_map(evoked_dip, fwd, cov, 0.1, return_as_dipoles=True)
amp_max = [np.max(d.amplitude) for d in dip_gmap]
dip_gmap = dip_gmap[np.argmax(amp_max)]
assert dip_gmap[0].pos[0] in src[0]['rr'][stc.vertices[0]]
dip_fit = mne.fit_dipole(evoked_dip, cov, sphere)[0]
assert np.abs(np.dot(dip_fit.ori[0], dip_gmap.ori[0])) > 0.99
```

## Next Steps


---

*Source: test_gamma_map.py:157 | Complexity: Advanced | Last updated: 2026-05-18*