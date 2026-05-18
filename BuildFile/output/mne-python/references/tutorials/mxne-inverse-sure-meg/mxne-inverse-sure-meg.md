# How To: Mxne Inverse Sure Meg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests SURE criterion for automatic alpha selection on MEG data.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne.datasets`
- `mne.dipole`
- `mne.inverse_sparse`
- `mne.inverse_sparse.mxne_inverse`
- `mne.inverse_sparse.mxne_optim`
- `mne.label`
- `mne.minimum_norm`
- `mne.minimum_norm.tests.test_inverse`
- `mne.simulation`
- `mne.source_estimate`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Tests SURE criterion for automatic alpha selection on MEG data.'

```python
'Tests SURE criterion for automatic alpha selection on MEG data.'
```

**Verification:**
```python
assert len(stc.vertices) == 2
```

### Step 2: Assign n_dipoles = 2

```python
n_dipoles = 2
```

**Verification:**
```python
assert_array_equal(stc.vertices[0], [89259])
```

### Step 3: Assign raw = mne.io.read_raw_fif.pick_types(...)

```python
raw = mne.io.read_raw_fif(fname_raw).pick_types('grad', exclude='bads')
```

**Verification:**
```python
assert_array_equal(stc.vertices[1], [70279])
```

### Step 4: Call raw.del_proj()

```python
raw.del_proj()
```

**Verification:**
```python
assert len(stc_.vertices) == len(stc.vertices) == 2
```

### Step 5: Assign info = value

```python
info = raw.info
```

**Verification:**
```python
assert_array_equal(stc_.vertices[si], stc.vertices[si], err_msg=f'si={si!r}')
```

### Step 6: Assign noise_cov = mne.make_ad_hoc_cov(...)

```python
noise_cov = mne.make_ad_hoc_cov(info)
```

### Step 7: Assign label_names = value

```python
label_names = ['Aud-lh', 'Aud-rh']
```

### Step 8: Assign labels = value

```python
labels = [mne.read_label(data_path / 'MEG' / 'sample' / 'labels' / f'{ln}.label') for ln in label_names]
```

### Step 9: Assign fname_fwd = value

```python
fname_fwd = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-meg-eeg-oct-4-fwd.fif'
```

### Step 10: Assign forward = mne.read_forward_solution(...)

```python
forward = mne.read_forward_solution(fname_fwd)
```

### Step 11: Assign forward = mne.pick_channels_forward(...)

```python
forward = mne.pick_channels_forward(forward, info['ch_names'])
```

### Step 12: Assign times = value

```python
times = np.arange(100, dtype=np.float64) / info['sfreq'] - 0.1
```

### Step 13: Assign stc = simulate_sparse_stc(...)

```python
stc = simulate_sparse_stc(forward['src'], n_dipoles=n_dipoles, times=times, random_state=1, labels=labels, data_fun=data_fun)
```

**Verification:**
```python
assert len(stc.vertices) == 2
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(stc.vertices[0], [89259])
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(stc.vertices[1], [70279])
```

### Step 16: Assign nave = 30

```python
nave = 30
```

### Step 17: Assign evoked = simulate_evoked(...)

```python
evoked = simulate_evoked(forward, stc, info, noise_cov, nave=nave, use_cps=False, iir_filter=None, random_state=0)
```

### Step 18: Assign evoked = evoked.crop(...)

```python
evoked = evoked.crop(tmin=0, tmax=0.01)
```

### Step 19: Assign stc_ = mixed_norm(...)

```python
stc_ = mixed_norm(evoked, forward, noise_cov, loose=0.9, n_mxne_iter=5, depth=0.9, random_state=1)
```

**Verification:**
```python
assert len(stc_.vertices) == len(stc.vertices) == 2
```

### Step 20: Assign data = np.zeros(...)

```python
data = np.zeros(times.shape)
```

### Step 21: Assign unknown = 5e-08

```python
data[times >= 0] = 5e-08
```

### Step 22: Call assert_array_equal()

```python
assert_array_equal(stc_.vertices[si], stc.vertices[si], err_msg=f'si={si!r}')
```


## Complete Example

```python
# Workflow
'Tests SURE criterion for automatic alpha selection on MEG data.'

def data_fun(times):
    data = np.zeros(times.shape)
    data[times >= 0] = 5e-08
    return data
n_dipoles = 2
raw = mne.io.read_raw_fif(fname_raw).pick_types('grad', exclude='bads')
raw.del_proj()
info = raw.info
del raw
noise_cov = mne.make_ad_hoc_cov(info)
label_names = ['Aud-lh', 'Aud-rh']
labels = [mne.read_label(data_path / 'MEG' / 'sample' / 'labels' / f'{ln}.label') for ln in label_names]
fname_fwd = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-meg-eeg-oct-4-fwd.fif'
forward = mne.read_forward_solution(fname_fwd)
forward = mne.pick_channels_forward(forward, info['ch_names'])
times = np.arange(100, dtype=np.float64) / info['sfreq'] - 0.1
stc = simulate_sparse_stc(forward['src'], n_dipoles=n_dipoles, times=times, random_state=1, labels=labels, data_fun=data_fun)
assert len(stc.vertices) == 2
assert_array_equal(stc.vertices[0], [89259])
assert_array_equal(stc.vertices[1], [70279])
nave = 30
evoked = simulate_evoked(forward, stc, info, noise_cov, nave=nave, use_cps=False, iir_filter=None, random_state=0)
evoked = evoked.crop(tmin=0, tmax=0.01)
stc_ = mixed_norm(evoked, forward, noise_cov, loose=0.9, n_mxne_iter=5, depth=0.9, random_state=1)
assert len(stc_.vertices) == len(stc.vertices) == 2
for si in range(len(stc_.vertices)):
    assert_array_equal(stc_.vertices[si], stc.vertices[si], err_msg=f'si={si!r}')
```

## Next Steps


---

*Source: test_mxne_inverse.py:558 | Complexity: Advanced | Last updated: 2026-05-18*