# How To: Lcmv Ctf Comp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test interpolation with compensated CTF data.

## Prerequisites

**Required Modules:**
- `contextlib`
- `copy`
- `inspect`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `scipy.spatial.distance`
- `mne`
- `mne`
- `mne._fiff.compensator`
- `mne._fiff.constants`
- `mne.beamformer`
- `mne.beamformer._compute_beamformer`
- `mne.datasets`
- `mne.fixes`
- `mne.minimum_norm`
- `mne.minimum_norm.tests.test_inverse`
- `mne.simulation`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test interpolation with compensated CTF data.'

```python
'Test interpolation with compensated CTF data.'
```

**Verification:**
```python
assert 'weights' in filters
```

### Step 2: Assign raw = mne.io.read_raw_ctf(...)

```python
raw = mne.io.read_raw_ctf(ctf_fname, preload=True)
```

### Step 3: Call raw.pick()

```python
raw.pick(raw.ch_names[:70])
```

### Step 4: Assign events = value

```python
events = mne.make_fixed_length_events(raw, duration=0.2)[:2]
```

### Step 5: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, tmin=-0.1, tmax=0.2)
```

### Step 6: Assign evoked = epochs.average(...)

```python
evoked = epochs.average()
```

### Step 7: Assign data_cov = mne.compute_covariance(...)

```python
data_cov = mne.compute_covariance(epochs)
```

### Step 8: Assign fwd = mne.make_forward_solution(...)

```python
fwd = mne.make_forward_solution(evoked.info, None, mne.setup_volume_source_space(pos=30.0), mne.make_sphere_model())
```

### Step 9: Assign filters = make_lcmv(...)

```python
filters = make_lcmv(evoked.info, fwd, data_cov, reduce_rank=True)
```

**Verification:**
```python
assert 'weights' in filters
```

### Step 10: Assign info_comp = evoked.info.copy(...)

```python
info_comp = evoked.info.copy()
```

### Step 11: Call set_current_comp()

```python
set_current_comp(info_comp, 1)
```

### Step 12: Call make_lcmv()

```python
make_lcmv(evoked.info, fwd, data_cov)
```

### Step 13: Call make_lcmv()

```python
make_lcmv(info_comp, fwd, data_cov)
```


## Complete Example

```python
# Workflow
'Test interpolation with compensated CTF data.'
raw = mne.io.read_raw_ctf(ctf_fname, preload=True)
raw.pick(raw.ch_names[:70])
events = mne.make_fixed_length_events(raw, duration=0.2)[:2]
epochs = mne.Epochs(raw, events, tmin=-0.1, tmax=0.2)
evoked = epochs.average()
data_cov = mne.compute_covariance(epochs)
fwd = mne.make_forward_solution(evoked.info, None, mne.setup_volume_source_space(pos=30.0), mne.make_sphere_model())
with pytest.raises(ValueError, match='reduce_rank'):
    make_lcmv(evoked.info, fwd, data_cov)
filters = make_lcmv(evoked.info, fwd, data_cov, reduce_rank=True)
assert 'weights' in filters
info_comp = evoked.info.copy()
set_current_comp(info_comp, 1)
with pytest.raises(RuntimeError, match='Compensation grade .* not match'):
    make_lcmv(info_comp, fwd, data_cov)
```

## Next Steps


---

*Source: test_lcmv.py:694 | Complexity: Advanced | Last updated: 2026-05-18*