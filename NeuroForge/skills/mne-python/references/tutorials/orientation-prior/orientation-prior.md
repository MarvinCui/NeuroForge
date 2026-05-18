# How To: Orientation Prior

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that orientation priors are handled properly.

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
# Fixtures: bias_params_free, method, looses, vmin, vmax, nmin, nmax
```

## Step-by-Step Guide

### Step 1: 'Test that orientation priors are handled properly.'

```python
'Test that orientation priors are handled properly.'
```

**Verification:**
```python
assert vec_stc is None
```

### Step 2: Assign unknown = bias_params_free

```python
evoked, fwd, noise_cov, _, _ = bias_params_free
```

**Verification:**
```python
assert vec_stc is not None
```

### Step 3: Assign stcs = list(...)

```python
stcs = list()
```

**Verification:**
```python
assert_allclose(stcs[1].data, vec_stc_normal.data)
```

### Step 4: Assign vec_stc = None

```python
vec_stc = None
```

**Verification:**
```python
assert_allclose(vec_stc_normal.data, vec_stc_surf[:, 2])
```

### Step 5: Assign rot = _normal_orth(...)

```python
rot = _normal_orth(np.concatenate([_get_src_nn(s) for s in inv['src']]))
```

**Verification:**
```python
assert_allclose(vec_stc_normal.data, stcs[1].data)
```

### Step 6: Assign vec_stc_surf = np.matmul(...)

```python
vec_stc_surf = np.matmul(rot, vec_stc.data)
```

**Verification:**
```python
assert nmin < ratio < nmax
```

### Step 7: Assign normal = np.linalg.norm(...)

```python
normal = np.linalg.norm(vec_stc_surf[:, 2].ravel())
```

**Verification:**
```python
assert stcs[0].data.shape == stcs[1].data.shape
```

### Step 8: Assign R2 = value

```python
R2 = 1.0 - np.linalg.norm(stcs[0].data.ravel() - stcs[1].data.ravel()) / np.linalg.norm(stcs[0].data.ravel())
```

**Verification:**
```python
assert vmin < R2 < vmax
```

### Step 9: Assign inv = make_inverse_operator(...)

```python
inv = make_inverse_operator(evoked.info, fwd, noise_cov, loose=loose)
```

### Step 10: Call stcs.append()

```python
stcs.append(apply_inverse(evoked, inv, method=method, pick_ori=pick_ori))
```

### Step 11: Assign unknown = vec_stc.project(...)

```python
vec_stc_normal, _ = vec_stc.project('normal', inv['src'])
```

### Step 12: Call assert_allclose()

```python
assert_allclose(stcs[1].data, vec_stc_normal.data)
```

### Step 13: Call assert_allclose()

```python
assert_allclose(vec_stc_normal.data, vec_stc_surf[:, 2])
```

### Step 14: Call assert_allclose()

```python
assert_allclose(vec_stc_normal.data, stcs[1].data)
```

### Step 15: Assign tangential = np.linalg.norm(...)

```python
tangential = np.linalg.norm(vec_stc_surf[:, ii].ravel())
```

### Step 16: Assign ratio = value

```python
ratio = normal / tangential
```

**Verification:**
```python
assert nmin < ratio < nmax
```

### Step 17: Assign pick_ori = value

```python
pick_ori = None if loose == 0 else 'normal'
```

### Step 18: Assign pick_ori = 'vector'

```python
pick_ori = 'vector'
```

**Verification:**
```python
assert vec_stc is None
```

### Step 19: Assign vec_stc = apply_inverse(...)

```python
vec_stc = apply_inverse(evoked, inv, method=method, pick_ori='vector')
```


## Complete Example

```python
# Setup
# Fixtures: bias_params_free, method, looses, vmin, vmax, nmin, nmax

# Workflow
'Test that orientation priors are handled properly.'
evoked, fwd, noise_cov, _, _ = bias_params_free
stcs = list()
vec_stc = None
for loose in looses:
    inv = make_inverse_operator(evoked.info, fwd, noise_cov, loose=loose)
    if looses[0] == 0.0:
        pick_ori = None if loose == 0 else 'normal'
    else:
        pick_ori = 'vector'
    stcs.append(apply_inverse(evoked, inv, method=method, pick_ori=pick_ori))
    if loose in (1.0, 0.2):
        assert vec_stc is None
        vec_stc = apply_inverse(evoked, inv, method=method, pick_ori='vector')
assert vec_stc is not None
rot = _normal_orth(np.concatenate([_get_src_nn(s) for s in inv['src']]))
vec_stc_surf = np.matmul(rot, vec_stc.data)
if 0.0 in looses:
    vec_stc_normal, _ = vec_stc.project('normal', inv['src'])
    assert_allclose(stcs[1].data, vec_stc_normal.data)
    del vec_stc
    assert_allclose(vec_stc_normal.data, vec_stc_surf[:, 2])
    assert_allclose(vec_stc_normal.data, stcs[1].data)
normal = np.linalg.norm(vec_stc_surf[:, 2].ravel())
for ii in range(2):
    tangential = np.linalg.norm(vec_stc_surf[:, ii].ravel())
    ratio = normal / tangential
    assert nmin < ratio < nmax
assert stcs[0].data.shape == stcs[1].data.shape
R2 = 1.0 - np.linalg.norm(stcs[0].data.ravel() - stcs[1].data.ravel()) / np.linalg.norm(stcs[0].data.ravel())
assert vmin < R2 < vmax
```

## Next Steps


---

*Source: test_inverse.py:734 | Complexity: Advanced | Last updated: 2026-05-18*