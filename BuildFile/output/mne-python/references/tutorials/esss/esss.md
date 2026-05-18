# How To: Esss

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test extended-basis SSS.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `re`
- `contextlib`
- `functools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.annotations`
- `mne.chpi`
- `mne.datasets`
- `mne.fixes`
- `mne.forward`
- `mne.io`
- `mne.preprocessing`
- `mne.preprocessing`
- `mne.preprocessing.maxwell`
- `mne.rank`
- `mne.utils`
- `scipy.io`

**Setup Required:**
```python
# Fixtures: regularize, bads
```

## Step-by-Step Guide

### Step 1: 'Test extended-basis SSS.'

```python
'Test extended-basis SSS.'
```

**Verification:**
```python
assert S_tot.shape[-1] == len(proj_sss)
```

### Step 2: Assign raw_erm = read_crop.load_data.pick(...)

```python
raw_erm = read_crop(erm_fname).load_data().pick('meg')
```

**Verification:**
```python
assert 'xtend' not in log
```

### Step 3: Assign unknown = bads

```python
raw_erm.info['bads'] = bads
```

**Verification:**
```python
assert 'Extending external SSS basis using 15 projection' in log
```

### Step 4: Assign proj_sss = mne.compute_proj_raw(...)

```python
proj_sss = mne.compute_proj_raw(raw_erm, meg='combined', verbose='error', n_mag=15, n_grad=15)
```

**Verification:**
```python
assert_allclose(raw_sss_2._data, raw_sss._data, atol=1e-20)
```

### Step 5: Assign good_info = pick_info(...)

```python
good_info = pick_info(raw_erm.info, pick_types(raw_erm.info, meg=True))
```

### Step 6: Assign S_tot = _trans_sss_basis(...)

```python
S_tot = _trans_sss_basis(dict(int_order=0, ext_order=3, origin=(0.0, 0.0, 0.0)), all_coils=_prep_mf_coils(good_info), coil_scale=1.0, trans=None)
```

**Verification:**
```python
assert S_tot.shape[-1] == len(proj_sss)
```

### Step 7: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'xtend' not in log
```

### Step 8: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'Extending external SSS basis using 15 projection' in log
```

### Step 9: Call assert_allclose()

```python
assert_allclose(raw_sss_2._data, raw_sss._data, atol=1e-20)
```

### Step 10: Assign unknown = value

```python
raw_erm.info['bads'] = raw_erm.info['bads'] + ['MEG0112']
```

### Step 11: Call maxwell_filter()

```python
maxwell_filter(raw_erm, coord_frame='meg', extended_proj=proj_sss)
```

### Step 12: Assign proj_sss = value

```python
proj_sss = proj_sss[:2]
```

### Step 13: Assign unknown = value

```python
proj_sss[0]['data']['col_names'] = proj_sss[0]['data']['col_names'][:-1]
```

### Step 14: Assign unknown = 1.0

```python
proj_sss[0] = 1.0
```

### Step 15: Assign unknown = b

```python
a['data']['data'][:] = b
```

### Step 16: Assign raw_sss = maxwell_filter(...)

```python
raw_sss = maxwell_filter(raw_erm, coord_frame='meg', regularize=regularize, verbose=True)
```

### Step 17: Assign raw_sss_2 = maxwell_filter(...)

```python
raw_sss_2 = maxwell_filter(raw_erm, coord_frame='meg', regularize=regularize, ext_order=0, extended_proj=proj_sss, verbose=True)
```

### Step 18: Call maxwell_filter()

```python
maxwell_filter(raw_erm, coord_frame='meg', extended_proj=proj_sss)
```

### Step 19: Call maxwell_filter()

```python
maxwell_filter(raw_erm, coord_frame='meg', extended_proj=proj_sss)
```

### Step 20: Call maxwell_filter()

```python
maxwell_filter(raw_erm, coord_frame='meg', extended_proj=1.0)
```


## Complete Example

```python
# Setup
# Fixtures: regularize, bads

# Workflow
'Test extended-basis SSS.'
raw_erm = read_crop(erm_fname).load_data().pick('meg')
raw_erm.info['bads'] = bads
proj_sss = mne.compute_proj_raw(raw_erm, meg='combined', verbose='error', n_mag=15, n_grad=15)
good_info = pick_info(raw_erm.info, pick_types(raw_erm.info, meg=True))
S_tot = _trans_sss_basis(dict(int_order=0, ext_order=3, origin=(0.0, 0.0, 0.0)), all_coils=_prep_mf_coils(good_info), coil_scale=1.0, trans=None)
assert S_tot.shape[-1] == len(proj_sss)
for a, b in zip(proj_sss, S_tot.T):
    a['data']['data'][:] = b
with catch_logging() as log:
    raw_sss = maxwell_filter(raw_erm, coord_frame='meg', regularize=regularize, verbose=True)
log = log.getvalue()
assert 'xtend' not in log
with catch_logging() as log:
    raw_sss_2 = maxwell_filter(raw_erm, coord_frame='meg', regularize=regularize, ext_order=0, extended_proj=proj_sss, verbose=True)
log = log.getvalue()
assert 'Extending external SSS basis using 15 projection' in log
assert_allclose(raw_sss_2._data, raw_sss._data, atol=1e-20)
raw_erm.info['bads'] = raw_erm.info['bads'] + ['MEG0112']
maxwell_filter(raw_erm, coord_frame='meg', extended_proj=proj_sss)
proj_sss = proj_sss[:2]
proj_sss[0]['data']['col_names'] = proj_sss[0]['data']['col_names'][:-1]
with pytest.raises(ValueError, match='were missing'):
    maxwell_filter(raw_erm, coord_frame='meg', extended_proj=proj_sss)
proj_sss[0] = 1.0
with pytest.raises(TypeError, match='extended_proj\\[0\\] must be an inst'):
    maxwell_filter(raw_erm, coord_frame='meg', extended_proj=proj_sss)
with pytest.raises(TypeError, match='extended_proj must be an inst'):
    maxwell_filter(raw_erm, coord_frame='meg', extended_proj=1.0)
```

## Next Steps


---

*Source: test_maxwell.py:1088 | Complexity: Advanced | Last updated: 2026-05-18*