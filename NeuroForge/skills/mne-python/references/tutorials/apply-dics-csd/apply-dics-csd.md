# How To: Apply Dics Csd

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test applying a DICS beamformer to a CSD matrix.

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
# Fixtures: _load_forward, idx, inversion, weight_norm
```

## Step-by-Step Guide

### Step 1: 'Test applying a DICS beamformer to a CSD matrix.'

```python
'Test applying a DICS beamformer to a CSD matrix.'
```

**Verification:**
```python
assert label.hemi == 'lh'
```

### Step 2: Assign unknown = _load_forward

```python
fwd_free, fwd_surf, fwd_fixed, _ = _load_forward
```

**Verification:**
```python
assert f == [10, 20]
```

### Step 3: Assign unknown = _simulate_data(...)

```python
epochs, _, csd, source_vertno, label, vertices, source_ind = _simulate_data(fwd_fixed, idx)
```

**Verification:**
```python
assert dist == 0.0
```

### Step 4: Assign reg = 1

```python
reg = 1
```

**Verification:**
```python
assert power.data[source_ind, 1] > power.data[source_ind, 0]
```

### Step 5: Call epochs.pick()

```python
epochs.pick(picks='grad')
```

**Verification:**
```python
assert label.hemi == 'lh'
```

### Step 6: Call make_dics()

```python
make_dics(epochs.info, fwd_free, csd)
```

### Step 7: Assign filters = make_dics(...)

```python
filters = make_dics(epochs.info, fwd, csd, label=label, reg=reg, inversion=inversion, weight_norm=weight_norm)
```

### Step 8: Assign unknown = apply_dics_csd(...)

```python
power, f = apply_dics_csd(csd, filters)
```

**Verification:**
```python
assert f == [10, 20]
```

### Step 9: Assign dist = _fwd_dist(...)

```python
dist = _fwd_dist(power, fwd_free, vertices, source_ind)
```

**Verification:**
```python
assert dist == 0.0
```


## Complete Example

```python
# Setup
# Fixtures: _load_forward, idx, inversion, weight_norm

# Workflow
'Test applying a DICS beamformer to a CSD matrix.'
fwd_free, fwd_surf, fwd_fixed, _ = _load_forward
epochs, _, csd, source_vertno, label, vertices, source_ind = _simulate_data(fwd_fixed, idx)
reg = 1
with pytest.raises(ValueError, match='several sensor types'):
    make_dics(epochs.info, fwd_free, csd)
epochs.pick(picks='grad')
assert label.hemi == 'lh'
for fwd in [fwd_free, fwd_surf, fwd_fixed]:
    filters = make_dics(epochs.info, fwd, csd, label=label, reg=reg, inversion=inversion, weight_norm=weight_norm)
    power, f = apply_dics_csd(csd, filters)
    assert f == [10, 20]
    dist = _fwd_dist(power, fwd_free, vertices, source_ind)
    assert dist == 0.0
    assert power.data[source_ind, 1] > power.data[source_ind, 0]
```

## Next Steps


---

*Source: test_dics.py:445 | Complexity: Advanced | Last updated: 2026-05-18*