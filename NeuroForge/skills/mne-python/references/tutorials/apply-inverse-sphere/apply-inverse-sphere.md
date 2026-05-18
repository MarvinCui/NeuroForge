# How To: Apply Inverse Sphere

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test applying an inverse with a sphere model (rank-deficient).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `re`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne.channels`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.fixes`
- `mne.forward`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.time_frequency`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: evoked, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test applying an inverse with a sphere model (rank-deficient).'

```python
'Test applying an inverse with a sphere model (rank-deficient).'
```

**Verification:**
```python
assert fwd['sol']['nrow'] == 39
```

### Step 2: Call evoked.pick()

```python
evoked.pick(evoked.ch_names[:306:8])
```

**Verification:**
```python
assert fwd['nsource'] == 101
```

### Step 3: Assign cov = make_ad_hoc_cov(...)

```python
cov = make_ad_hoc_cov(evoked.info)
```

**Verification:**
```python
assert fwd['sol']['ncol'] == 303
```

### Step 4: Assign sphere = make_sphere_model(...)

```python
sphere = make_sphere_model((0.0, 0.0, 0.04), None)
```

**Verification:**
```python
assert_array_equal(np.argmax(stc.data, axis=0), np.repeat(np.arange(101), 3))
```

### Step 5: Assign fwd = read_forward_solution(...)

```python
fwd = read_forward_solution(fname_fwd)
```

### Step 6: Assign vertices = value

```python
vertices = [fwd['src'][0]['vertno'][::5], fwd['src'][1]['vertno'][::5]]
```

### Step 7: Assign stc = SourceEstimate(...)

```python
stc = SourceEstimate(np.zeros((sum((len(v) for v in vertices)), 1)), vertices, 0.0, 1.0)
```

### Step 8: Assign fwd = restrict_forward_to_stc(...)

```python
fwd = restrict_forward_to_stc(fwd, stc)
```

### Step 9: Assign fwd = make_forward_solution(...)

```python
fwd = make_forward_solution(evoked.info, fwd['mri_head_t'], fwd['src'], sphere, mindist=5.0)
```

### Step 10: Assign evoked = EvokedArray(...)

```python
evoked = EvokedArray(fwd['sol']['data'].copy(), evoked.info)
```

**Verification:**
```python
assert fwd['sol']['nrow'] == 39
```

### Step 11: Assign temp_fname = value

```python
temp_fname = tmp_path / 'temp-inv.fif'
```

### Step 12: Assign inv = make_inverse_operator(...)

```python
inv = make_inverse_operator(evoked.info, fwd, cov, loose=1.0)
```

### Step 13: Call write_inverse_operator()

```python
write_inverse_operator(temp_fname, inv)
```

### Step 14: Assign inv = read_inverse_operator(...)

```python
inv = read_inverse_operator(temp_fname)
```

### Step 15: Assign stc = apply_inverse(...)

```python
stc = apply_inverse(evoked, inv, method='eLORETA', method_params=dict(eps=0.01))
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(np.argmax(stc.data, axis=0), np.repeat(np.arange(101), 3))
```

### Step 17: Assign unknown = value

```python
evoked.info['projs'] = []
```


## Complete Example

```python
# Setup
# Fixtures: evoked, tmp_path

# Workflow
'Test applying an inverse with a sphere model (rank-deficient).'
evoked.pick(evoked.ch_names[:306:8])
with evoked.info._unlock():
    evoked.info['projs'] = []
cov = make_ad_hoc_cov(evoked.info)
sphere = make_sphere_model((0.0, 0.0, 0.04), None)
fwd = read_forward_solution(fname_fwd)
vertices = [fwd['src'][0]['vertno'][::5], fwd['src'][1]['vertno'][::5]]
stc = SourceEstimate(np.zeros((sum((len(v) for v in vertices)), 1)), vertices, 0.0, 1.0)
fwd = restrict_forward_to_stc(fwd, stc)
fwd = make_forward_solution(evoked.info, fwd['mri_head_t'], fwd['src'], sphere, mindist=5.0)
evoked = EvokedArray(fwd['sol']['data'].copy(), evoked.info)
assert fwd['sol']['nrow'] == 39
assert fwd['nsource'] == 101
assert fwd['sol']['ncol'] == 303
temp_fname = tmp_path / 'temp-inv.fif'
inv = make_inverse_operator(evoked.info, fwd, cov, loose=1.0)
write_inverse_operator(temp_fname, inv)
inv = read_inverse_operator(temp_fname)
stc = apply_inverse(evoked, inv, method='eLORETA', method_params=dict(eps=0.01))
assert_array_equal(np.argmax(stc.data, axis=0), np.repeat(np.arange(101), 3))
```

## Next Steps


---

*Source: test_inverse.py:574 | Complexity: Advanced | Last updated: 2026-05-18*