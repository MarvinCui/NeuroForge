# How To: Magnetic Dipole

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test basic magnetic dipole forward calculation.

## Prerequisites

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.datasets`
- `mne.dipole`
- `mne.forward`
- `mne.forward._compute_forward`
- `mne.forward._make_forward`
- `mne.forward.tests.test_forward`
- `mne.io`
- `mne.simulation`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test basic magnetic dipole forward calculation.'

```python
'Test basic magnetic dipole forward calculation.'
```

**Verification:**
```python
assert_allclose(np.median(near_fwd / far_fwd), ratio, atol=0.1)
```

### Step 2: Assign info = read_info(...)

```python
info = read_info(fname_raw)
```

**Verification:**
```python
assert not np.isfinite(fwd).any()
```

### Step 3: Assign picks = pick_types(...)

```python
picks = pick_types(info, meg=True, eeg=False, exclude=[])
```

**Verification:**
```python
assert not np.isfinite(fwd).any()
```

### Step 4: Assign info = pick_info(...)

```python
info = pick_info(info, picks[:12])
```

### Step 5: Assign coils = _create_meg_coils(...)

```python
coils = _create_meg_coils(info['chs'], 'normal', None)
```

### Step 6: Assign r0 = np.array(...)

```python
r0 = np.array([0.0, 13.0, -6.0])
```

### Step 7: Assign r0 = value

```python
r0 = coils[0]['rmag'][[0]]
```

**Verification:**
```python
assert not np.isfinite(fwd).any()
```

### Step 8: Assign rr = value

```python
rr = (ch['loc'][:3] + r0) / 2.0
```

### Step 9: Assign far_fwd = _magnetic_dipole_field_vec(...)

```python
far_fwd = _magnetic_dipole_field_vec(r0[np.newaxis, :], [coil])
```

### Step 10: Assign near_fwd = _magnetic_dipole_field_vec(...)

```python
near_fwd = _magnetic_dipole_field_vec(rr[np.newaxis, :], [coil])
```

### Step 11: Assign ratio = value

```python
ratio = 8.0 if ch['ch_name'][-1] == '1' else 16.0
```

### Step 12: Call assert_allclose()

```python
assert_allclose(np.median(near_fwd / far_fwd), ratio, atol=0.1)
```

### Step 13: Call _magnetic_dipole_field_vec()

```python
_magnetic_dipole_field_vec(r0, coils[:1])
```

### Step 14: Assign fwd = _magnetic_dipole_field_vec(...)

```python
fwd = _magnetic_dipole_field_vec(r0, coils[:1], too_close='warning')
```

### Step 15: Assign fwd = _magnetic_dipole_field_vec(...)

```python
fwd = _magnetic_dipole_field_vec(r0, coils[:1], too_close='info')
```


## Complete Example

```python
# Workflow
'Test basic magnetic dipole forward calculation.'
info = read_info(fname_raw)
picks = pick_types(info, meg=True, eeg=False, exclude=[])
info = pick_info(info, picks[:12])
coils = _create_meg_coils(info['chs'], 'normal', None)
r0 = np.array([0.0, 13.0, -6.0])
for ch, coil in zip(info['chs'], coils):
    rr = (ch['loc'][:3] + r0) / 2.0
    far_fwd = _magnetic_dipole_field_vec(r0[np.newaxis, :], [coil])
    near_fwd = _magnetic_dipole_field_vec(rr[np.newaxis, :], [coil])
    ratio = 8.0 if ch['ch_name'][-1] == '1' else 16.0
    assert_allclose(np.median(near_fwd / far_fwd), ratio, atol=0.1)
r0 = coils[0]['rmag'][[0]]
with pytest.raises(RuntimeError, match='Coil too close'):
    _magnetic_dipole_field_vec(r0, coils[:1])
with _record_warnings(), pytest.warns(RuntimeWarning, match='Coil too close'):
    fwd = _magnetic_dipole_field_vec(r0, coils[:1], too_close='warning')
assert not np.isfinite(fwd).any()
with np.errstate(invalid='ignore'):
    fwd = _magnetic_dipole_field_vec(r0, coils[:1], too_close='info')
assert not np.isfinite(fwd).any()
```

## Next Steps


---

*Source: test_make_forward.py:190 | Complexity: Advanced | Last updated: 2026-05-18*