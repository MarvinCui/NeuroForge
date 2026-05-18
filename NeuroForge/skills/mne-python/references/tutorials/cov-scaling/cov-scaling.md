# How To: Cov Scaling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test rescaling covs.

## Prerequisites

**Required Modules:**
- `copy`
- `datetime`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.epochs`
- `mne.fixes`
- `mne.io`
- `mne.time_frequency`
- `mne.utils`
- `mne.utils.numerics`
- `sklearn.decomposition`


## Step-by-Step Guide

### Step 1: 'Test rescaling covs.'

```python
'Test rescaling covs.'
```

**Verification:**
```python
assert_array_equal(cov, cov2)
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(ave_fname, condition=0, baseline=(None, 0), proj=True)
```

**Verification:**
```python
assert_array_equal(cov, cov2)
```

### Step 3: Assign cov = value

```python
cov = read_cov(cov_fname)['data']
```

**Verification:**
```python
assert cov.max() > 1
```

### Step 4: Assign cov2 = value

```python
cov2 = read_cov(cov_fname)['data']
```

**Verification:**
```python
assert_array_equal(cov, cov2)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(cov, cov2)
```

**Verification:**
```python
assert cov.max() < 1
```

### Step 6: Call evoked.pick()

```python
evoked.pick([evoked.ch_names[k] for k in pick_types(evoked.info, meg=True, eeg=True)])
```

**Verification:**
```python
assert_allclose(data, evoked.data, atol=1e-20)
```

### Step 7: Assign picks_list = _picks_by_type(...)

```python
picks_list = _picks_by_type(evoked.info)
```

### Step 8: Assign scalings = dict(...)

```python
scalings = dict(mag=1000000000000000.0, grad=10000000000000.0, eeg=1000000.0)
```

### Step 9: Call _apply_scaling_cov()

```python
_apply_scaling_cov(cov2, picks_list, scalings=scalings)
```

### Step 10: Call _apply_scaling_cov()

```python
_apply_scaling_cov(cov, picks_list, scalings=scalings)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(cov, cov2)
```

**Verification:**
```python
assert cov.max() > 1
```

### Step 12: Call _undo_scaling_cov()

```python
_undo_scaling_cov(cov2, picks_list, scalings=scalings)
```

### Step 13: Call _undo_scaling_cov()

```python
_undo_scaling_cov(cov, picks_list, scalings=scalings)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(cov, cov2)
```

**Verification:**
```python
assert cov.max() < 1
```

### Step 15: Assign data = evoked.data.copy(...)

```python
data = evoked.data.copy()
```

### Step 16: Call _apply_scaling_array()

```python
_apply_scaling_array(data, picks_list, scalings=scalings)
```

### Step 17: Call _undo_scaling_array()

```python
_undo_scaling_array(data, picks_list, scalings=scalings)
```

### Step 18: Call assert_allclose()

```python
assert_allclose(data, evoked.data, atol=1e-20)
```


## Complete Example

```python
# Workflow
'Test rescaling covs.'
evoked = read_evokeds(ave_fname, condition=0, baseline=(None, 0), proj=True)
cov = read_cov(cov_fname)['data']
cov2 = read_cov(cov_fname)['data']
assert_array_equal(cov, cov2)
evoked.pick([evoked.ch_names[k] for k in pick_types(evoked.info, meg=True, eeg=True)])
picks_list = _picks_by_type(evoked.info)
scalings = dict(mag=1000000000000000.0, grad=10000000000000.0, eeg=1000000.0)
_apply_scaling_cov(cov2, picks_list, scalings=scalings)
_apply_scaling_cov(cov, picks_list, scalings=scalings)
assert_array_equal(cov, cov2)
assert cov.max() > 1
_undo_scaling_cov(cov2, picks_list, scalings=scalings)
_undo_scaling_cov(cov, picks_list, scalings=scalings)
assert_array_equal(cov, cov2)
assert cov.max() < 1
data = evoked.data.copy()
_apply_scaling_array(data, picks_list, scalings=scalings)
_undo_scaling_array(data, picks_list, scalings=scalings)
assert_allclose(data, evoked.data, atol=1e-20)
```

## Next Steps


---

*Source: test_numerics.py:227 | Complexity: Advanced | Last updated: 2026-05-18*