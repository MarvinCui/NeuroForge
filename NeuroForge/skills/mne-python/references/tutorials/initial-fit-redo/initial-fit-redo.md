# How To: Initial Fit Redo

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that initial fits can be redone based on moments.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.interpolate`
- `scipy.spatial.distance`
- `mne`
- `mne._fiff.constants`
- `mne.chpi`
- `mne.datasets`
- `mne.forward._compute_forward`
- `mne.io`
- `mne.simulation`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz`
- `scipy.signal`


## Step-by-Step Guide

### Step 1: 'Test that initial fits can be redone based on moments.'

```python
'Test that initial fits can be redone based on moments.'
```

**Verification:**
```python
assert_array_less(amps, 5e-11)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes')
```

**Verification:**
```python
assert_array_less(1e-12, amps)
```

### Step 3: Assign slopes = np.array(...)

```python
slopes = np.array([[c['slopes'] for c in raw.info['hpi_meas'][0]['hpi_coils']]])
```

**Verification:**
```python
assert_allclose(chpi_locs['gofs'][0], coil_gof, atol=0.3)
```

### Step 4: Assign amps = np.linalg.norm(...)

```python
amps = np.linalg.norm(slopes, axis=-1)
```

**Verification:**
```python
assert_allclose(coil_amp, py_amp, rtol=0.2)
```

### Step 5: Call assert_array_less()

```python
assert_array_less(amps, 5e-11)
```

**Verification:**
```python
assert_array_less(angles, 20)
```

### Step 6: Call assert_array_less()

```python
assert_array_less(1e-12, amps)
```

**Verification:**
```python
assert head_pos.shape == (1, 10)
```

### Step 7: Assign unknown = _setup_ext_proj(...)

```python
proj, _, _ = _setup_ext_proj(raw.info, ext_order=1)
```

**Verification:**
```python
assert 0.1 < dist < 2
```

### Step 8: Assign chpi_amplitudes = dict(...)

```python
chpi_amplitudes = dict(times=np.zeros(1), slopes=slopes, proj=proj)
```

**Verification:**
```python
assert 0.1 < angle < 2
```

### Step 9: Assign chpi_locs = compute_chpi_locs(...)

```python
chpi_locs = compute_chpi_locs(raw.info, chpi_amplitudes)
```

**Verification:**
```python
assert_allclose(gof, 0.9999, atol=0.0001)
```

### Step 10: Assign coil_gof = value

```python
coil_gof = raw.info['hpi_results'][0]['goodness']
```

### Step 11: Call assert_allclose()

```python
assert_allclose(chpi_locs['gofs'][0], coil_gof, atol=0.3)
```

### Step 12: Assign coil_moment = value

```python
coil_moment = raw.info['hpi_results'][0]['moments'] / _MAG_FACTOR
```

### Step 13: Assign py_moment = value

```python
py_moment = chpi_locs['moments'][0]
```

### Step 14: Assign coil_amp = np.linalg.norm(...)

```python
coil_amp = np.linalg.norm(coil_moment, axis=-1, keepdims=True)
```

### Step 15: Assign py_amp = np.linalg.norm(...)

```python
py_amp = np.linalg.norm(py_moment, axis=-1, keepdims=True)
```

### Step 16: Call assert_allclose()

```python
assert_allclose(coil_amp, py_amp, rtol=0.2)
```

### Step 17: Assign coil_ori = value

```python
coil_ori = coil_moment / coil_amp
```

### Step 18: Assign py_ori = value

```python
py_ori = py_moment / py_amp
```

### Step 19: Assign angles = np.rad2deg(...)

```python
angles = np.rad2deg(np.arccos(np.abs(np.sum(coil_ori * py_ori, axis=1))))
```

### Step 20: Call assert_array_less()

```python
assert_array_less(angles, 20)
```

### Step 21: Assign head_pos = compute_head_pos(...)

```python
head_pos = compute_head_pos(raw.info, chpi_locs)
```

**Verification:**
```python
assert head_pos.shape == (1, 10)
```

### Step 22: Assign nm_pos = value

```python
nm_pos = raw.info['dev_head_t']['trans']
```

### Step 23: Assign dist = value

```python
dist = 1000 * np.linalg.norm(nm_pos[:3, 3] - head_pos[0, 4:7])
```

**Verification:**
```python
assert 0.1 < dist < 2
```

### Step 24: Assign angle = np.rad2deg(...)

```python
angle = np.rad2deg(_angle_between_quats(rot_to_quat(nm_pos[:3, :3]), head_pos[0, 1:4]))
```

**Verification:**
```python
assert 0.1 < angle < 2
```

### Step 25: Assign gof = value

```python
gof = head_pos[0, 7]
```

### Step 26: Call assert_allclose()

```python
assert_allclose(gof, 0.9999, atol=0.0001)
```


## Complete Example

```python
# Workflow
'Test that initial fits can be redone based on moments.'
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes')
slopes = np.array([[c['slopes'] for c in raw.info['hpi_meas'][0]['hpi_coils']]])
amps = np.linalg.norm(slopes, axis=-1)
amps /= slopes.shape[-1]
assert_array_less(amps, 5e-11)
assert_array_less(1e-12, amps)
proj, _, _ = _setup_ext_proj(raw.info, ext_order=1)
chpi_amplitudes = dict(times=np.zeros(1), slopes=slopes, proj=proj)
chpi_locs = compute_chpi_locs(raw.info, chpi_amplitudes)
coil_gof = raw.info['hpi_results'][0]['goodness']
assert_allclose(chpi_locs['gofs'][0], coil_gof, atol=0.3)
coil_moment = raw.info['hpi_results'][0]['moments'] / _MAG_FACTOR
py_moment = chpi_locs['moments'][0]
coil_amp = np.linalg.norm(coil_moment, axis=-1, keepdims=True)
py_amp = np.linalg.norm(py_moment, axis=-1, keepdims=True)
assert_allclose(coil_amp, py_amp, rtol=0.2)
coil_ori = coil_moment / coil_amp
py_ori = py_moment / py_amp
angles = np.rad2deg(np.arccos(np.abs(np.sum(coil_ori * py_ori, axis=1))))
assert_array_less(angles, 20)
head_pos = compute_head_pos(raw.info, chpi_locs)
assert head_pos.shape == (1, 10)
nm_pos = raw.info['dev_head_t']['trans']
dist = 1000 * np.linalg.norm(nm_pos[:3, 3] - head_pos[0, 4:7])
assert 0.1 < dist < 2
angle = np.rad2deg(_angle_between_quats(rot_to_quat(nm_pos[:3, :3]), head_pos[0, 1:4]))
assert 0.1 < angle < 2
gof = head_pos[0, 7]
assert_allclose(gof, 0.9999, atol=0.0001)
```

## Next Steps


---

*Source: test_chpi.py:447 | Complexity: Advanced | Last updated: 2026-05-18*