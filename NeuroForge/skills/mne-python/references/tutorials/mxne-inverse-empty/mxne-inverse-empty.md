# How To: Mxne Inverse Empty

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests solver with too high alpha.

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

### Step 1: 'Tests solver with too high alpha.'

```python
'Tests solver with too high alpha.'
```

**Verification:**
```python
assert stc.data.size == 0
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(fname_data, condition=0, baseline=(None, 0))
```

**Verification:**
```python
assert stc.vertices[0].size == 0
```

### Step 3: Call evoked.pick()

```python
evoked.pick('grad', exclude='bads')
```

**Verification:**
```python
assert stc.vertices[1].size == 0
```

### Step 4: Assign fname_fwd = value

```python
fname_fwd = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-meg-eeg-oct-4-fwd.fif'
```

**Verification:**
```python
assert_allclose(evoked.data, residual.data)
```

### Step 5: Assign forward = mne.read_forward_solution(...)

```python
forward = mne.read_forward_solution(fname_fwd)
```

### Step 6: Assign forward = mne.pick_types_forward(...)

```python
forward = mne.pick_types_forward(forward, meg='grad', eeg=False, exclude=evoked.info['bads'])
```

### Step 7: Assign cov = read_cov(...)

```python
cov = read_cov(fname_cov)
```

### Step 8: Assign unknown = mixed_norm(...)

```python
stc, residual = mixed_norm(evoked, forward, cov, n_mxne_iter=3, alpha=99, return_residual=True, random_state=0)
```

**Verification:**
```python
assert stc.data.size == 0
```

### Step 9: Call assert_allclose()

```python
assert_allclose(evoked.data, residual.data)
```


## Complete Example

```python
# Workflow
'Tests solver with too high alpha.'
evoked = read_evokeds(fname_data, condition=0, baseline=(None, 0))
evoked.pick('grad', exclude='bads')
fname_fwd = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-meg-eeg-oct-4-fwd.fif'
forward = mne.read_forward_solution(fname_fwd)
forward = mne.pick_types_forward(forward, meg='grad', eeg=False, exclude=evoked.info['bads'])
cov = read_cov(fname_cov)
with pytest.warns(RuntimeWarning, match='too big'):
    stc, residual = mixed_norm(evoked, forward, cov, n_mxne_iter=3, alpha=99, return_residual=True, random_state=0)
    assert stc.data.size == 0
    assert stc.vertices[0].size == 0
    assert stc.vertices[1].size == 0
    assert_allclose(evoked.data, residual.data)
```

## Next Steps


---

*Source: test_mxne_inverse.py:616 | Complexity: Advanced | Last updated: 2026-05-18*