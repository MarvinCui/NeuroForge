# How To: Real

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test using a real-valued filter.

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
# Fixtures: _load_forward, idx
```

## Step-by-Step Guide

### Step 1: 'Test using a real-valued filter.'

```python
'Test using a real-valued filter.'
```

**Verification:**
```python
assert f == [10, 20]
```

### Step 2: Assign unknown = _load_forward

```python
fwd_free, fwd_surf, fwd_fixed, fwd_vol = _load_forward
```

**Verification:**
```python
assert dist == 0
```

### Step 3: Assign unknown = _simulate_data(...)

```python
epochs, _, csd, source_vertno, label, vertices, source_ind = _simulate_data(fwd_fixed, idx)
```

**Verification:**
```python
assert power.data[source_ind, 1] > power.data[source_ind, 0]
```

### Step 4: Call epochs.pick()

```python
epochs.pick(picks='grad')
```

**Verification:**
```python
assert f == [10, 20]
```

### Step 5: Assign reg = 1

```python
reg = 1
```

**Verification:**
```python
assert dist == 0
```

### Step 6: Assign filters_real = make_dics(...)

```python
filters_real = make_dics(epochs.info, fwd_surf, csd, label=label, reg=reg, real_filter=True, inversion='single')
```

**Verification:**
```python
assert power.data[source_ind, 1] > power.data[source_ind, 0]
```

### Step 7: Assign unknown = apply_dics_csd(...)

```python
power, f = apply_dics_csd(csd, filters_real)
```

**Verification:**
```python
assert f == [10, 20]
```

### Step 8: Assign dist = _fwd_dist(...)

```python
dist = _fwd_dist(power, fwd_surf, vertices, source_ind)
```

**Verification:**
```python
assert dist <= vol_tols.get(idx, 0.0)
```

### Step 9: Assign filters_real = make_dics(...)

```python
filters_real = make_dics(epochs.info, fwd_surf, csd, label=label, reg=5, pick_ori='max-power', inversion='matrix', reduce_rank=True)
```

**Verification:**
```python
assert power.data[vol_source_ind, 1] > power.data[vol_source_ind, 0]
```

### Step 10: Assign unknown = apply_dics_csd(...)

```python
power, f = apply_dics_csd(csd, filters_real)
```

**Verification:**
```python
assert f == [10, 20]
```

### Step 11: Assign dist = _fwd_dist(...)

```python
dist = _fwd_dist(power, fwd_surf, vertices, source_ind)
```

**Verification:**
```python
assert dist == 0
```

### Step 12: Assign filters_vol = make_dics(...)

```python
filters_vol = make_dics(epochs.info, fwd_vol, csd, reg=reg, inversion='single')
```

### Step 13: Assign unknown = apply_dics_csd(...)

```python
power, f = apply_dics_csd(csd, filters_vol)
```

### Step 14: Assign vol_source_ind = _nearest_vol_ind(...)

```python
vol_source_ind = _nearest_vol_ind(fwd_vol, fwd_surf, vertices, source_ind)
```

**Verification:**
```python
assert f == [10, 20]
```

### Step 15: Assign dist = _fwd_dist(...)

```python
dist = _fwd_dist(power, fwd_vol, fwd_vol['src'][0]['vertno'], vol_source_ind)
```

### Step 16: Assign vol_tols = value

```python
vol_tols = {100: 0.008, 200: 0.008}
```

**Verification:**
```python
assert dist <= vol_tols.get(idx, 0.0)
```

### Step 17: Call apply_dics_csd()

```python
apply_dics_csd(csd, filters_vol)
```


## Complete Example

```python
# Setup
# Fixtures: _load_forward, idx

# Workflow
'Test using a real-valued filter.'
fwd_free, fwd_surf, fwd_fixed, fwd_vol = _load_forward
epochs, _, csd, source_vertno, label, vertices, source_ind = _simulate_data(fwd_fixed, idx)
epochs.pick(picks='grad')
reg = 1
filters_real = make_dics(epochs.info, fwd_surf, csd, label=label, reg=reg, real_filter=True, inversion='single')
power, f = apply_dics_csd(csd, filters_real)
assert f == [10, 20]
dist = _fwd_dist(power, fwd_surf, vertices, source_ind)
assert dist == 0
assert power.data[source_ind, 1] > power.data[source_ind, 0]
filters_real = make_dics(epochs.info, fwd_surf, csd, label=label, reg=5, pick_ori='max-power', inversion='matrix', reduce_rank=True)
power, f = apply_dics_csd(csd, filters_real)
assert f == [10, 20]
dist = _fwd_dist(power, fwd_surf, vertices, source_ind)
assert dist == 0
assert power.data[source_ind, 1] > power.data[source_ind, 0]
filters_vol = make_dics(epochs.info, fwd_vol, csd, reg=reg, inversion='single')
power, f = apply_dics_csd(csd, filters_vol)
vol_source_ind = _nearest_vol_ind(fwd_vol, fwd_surf, vertices, source_ind)
assert f == [10, 20]
dist = _fwd_dist(power, fwd_vol, fwd_vol['src'][0]['vertno'], vol_source_ind)
vol_tols = {100: 0.008, 200: 0.008}
assert dist <= vol_tols.get(idx, 0.0)
assert power.data[vol_source_ind, 1] > power.data[vol_source_ind, 0]
del filters_vol['src_type']
with pytest.warns(RuntimeWarning, match='spatial filter does not contain src_type'):
    apply_dics_csd(csd, filters_vol)
```

## Next Steps


---

*Source: test_dics.py:547 | Complexity: Advanced | Last updated: 2026-05-18*