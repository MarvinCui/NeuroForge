# How To: Lcmv Fieldtrip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test LCMV vs fieldtrip output.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne.beamformer`
- `mne.beamformer.tests.test_lcmv`
- `mne.datasets`
- `mne.fixes`

**Setup Required:**
```python
# Fixtures: _get_bf_data, bf_type, weight_norm, pick_ori, pwr
```

## Step-by-Step Guide

### Step 1: 'Test LCMV vs fieldtrip output.'

```python
'Test LCMV vs fieldtrip output.'
```

**Verification:**
```python
assert_array_equal(signs, 1.0)
```

### Step 2: Assign pymatreader = pytest.importorskip(...)

```python
pymatreader = pytest.importorskip('pymatreader')
```

**Verification:**
```python
assert stc_ft_data.shape == stc_mne.data.shape
```

### Step 3: Assign unknown = _get_bf_data

```python
evoked, data_cov, fwd = _get_bf_data
```

**Verification:**
```python
assert_allclose(np.linalg.norm(stc_mne.data, axis=1), np.linalg.norm(stc_ft_data, axis=1), rtol=1e-06)
```

### Step 4: Assign filters = make_lcmv(...)

```python
filters = make_lcmv(evoked.info, fwd, data_cov=data_cov, noise_cov=None, pick_ori=pick_ori, reg=0.05, weight_norm=weight_norm)
```

**Verification:**
```python
assert_allclose(stc_mne.data, stc_ft_data, rtol=1e-06)
```

### Step 5: Assign ft_fname = value

```python
ft_fname = ft_data_path / ('ft_source_' + bf_type + '-vol.mat')
```

### Step 6: Assign stc_ft_data = value

```python
stc_ft_data = pymatreader.read_mat(ft_fname)['stc']
```

**Verification:**
```python
assert stc_ft_data.shape == stc_mne.data.shape
```

### Step 7: Call assert_allclose()

```python
assert_allclose(stc_mne.data, stc_ft_data, rtol=1e-06)
```

### Step 8: Assign stc_mne = apply_lcmv_cov(...)

```python
stc_mne = apply_lcmv_cov(data_cov, filters)
```

### Step 9: Assign stc_mne = apply_lcmv(...)

```python
stc_mne = apply_lcmv(evoked, filters)
```

### Step 10: Assign stc_ft_data = _reshape_view(...)

```python
stc_ft_data = _reshape_view(stc_ft_data, (stc_ft_data.size, 1))
```

### Step 11: Assign signs = np.sign(...)

```python
signs = np.sign((stc_mne.data * stc_ft_data).sum(-1, keepdims=True))
```

### Step 12: Call assert_allclose()

```python
assert_allclose(np.linalg.norm(stc_mne.data, axis=1), np.linalg.norm(stc_ft_data, axis=1), rtol=1e-06)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(signs, 1.0)
```


## Complete Example

```python
# Setup
# Fixtures: _get_bf_data, bf_type, weight_norm, pick_ori, pwr

# Workflow
'Test LCMV vs fieldtrip output.'
pymatreader = pytest.importorskip('pymatreader')
evoked, data_cov, fwd = _get_bf_data
filters = make_lcmv(evoked.info, fwd, data_cov=data_cov, noise_cov=None, pick_ori=pick_ori, reg=0.05, weight_norm=weight_norm)
if pwr:
    stc_mne = apply_lcmv_cov(data_cov, filters)
else:
    stc_mne = apply_lcmv(evoked, filters)
ft_fname = ft_data_path / ('ft_source_' + bf_type + '-vol.mat')
stc_ft_data = pymatreader.read_mat(ft_fname)['stc']
if stc_ft_data.ndim == 1:
    stc_ft_data = _reshape_view(stc_ft_data, (stc_ft_data.size, 1))
if stc_mne.data.ndim == 2:
    signs = np.sign((stc_mne.data * stc_ft_data).sum(-1, keepdims=True))
    if pwr:
        assert_array_equal(signs, 1.0)
    stc_mne.data *= signs
assert stc_ft_data.shape == stc_mne.data.shape
if pick_ori == 'vector':
    assert_allclose(np.linalg.norm(stc_mne.data, axis=1), np.linalg.norm(stc_ft_data, axis=1), rtol=1e-06)
assert_allclose(stc_mne.data, stc_ft_data, rtol=1e-06)
```

## Next Steps


---

*Source: test_external.py:77 | Complexity: Advanced | Last updated: 2026-05-18*