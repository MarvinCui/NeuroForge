# How To: Calculate Chpi Coil Locs Artemis

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test computing just cHPI locations.

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

### Step 1: 'Test computing just cHPI locations.'

```python
'Test computing just cHPI locations.'
```

**Verification:**
```python
assert_allclose(times[0], 9.0, atol=0.01)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes', preload=True)
```

**Verification:**
```python
assert_allclose(cHPI_digs[0][2]['r'], [-0.01937833, 0.00346804, 0.06331209], atol=0.001)
```

### Step 3: Assign raw_dec = _decimate_chpi(...)

```python
raw_dec = _decimate_chpi(raw, 15)
```

**Verification:**
```python
assert_allclose(cHPI_digs[0][2]['gof'], 0.9957, atol=0.001)
```

### Step 4: Assign unknown = _calculate_chpi_coil_locs(...)

```python
times, cHPI_digs = _calculate_chpi_coil_locs(raw_dec, verbose='debug')
```

**Verification:**
```python
assert_allclose(cHPI_digs[0][4]['r'], [-0.0655, 0.0755, 0.0004], atol=0.003)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(times[0], 9.0, atol=0.01)
```

**Verification:**
```python
assert_allclose(cHPI_digs[0][4]['gof'], 0.9323, atol=0.001)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(cHPI_digs[0][2]['r'], [-0.01937833, 0.00346804, 0.06331209], atol=0.001)
```

**Verification:**
```python
assert len(np.setdiff1d(times, raw.times + raw.first_time)) == 0
```

### Step 7: Call assert_allclose()

```python
assert_allclose(cHPI_digs[0][2]['gof'], 0.9957, atol=0.001)
```

**Verification:**
```python
assert_allclose(times[5], 1.5, atol=0.2)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(cHPI_digs[0][4]['r'], [-0.0655, 0.0755, 0.0004], atol=0.003)
```

**Verification:**
```python
assert_allclose(cHPI_digs[5][0]['gof'], 0.995, atol=0.005)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(cHPI_digs[0][4]['gof'], 0.9323, atol=0.001)
```

**Verification:**
```python
assert_allclose(cHPI_digs[5][0]['r'], [-0.0157, 0.0655, 0.0018], atol=0.001)
```

### Step 10: Call _check_dists()

```python
_check_dists(raw.info, cHPI_digs[0], n_bad=1)
```

**Verification:**
```python
assert amps.shape == (len(coil_amplitudes['times']), 3)
```

### Step 11: Assign raw = read_raw_artemis123(...)

```python
raw = read_raw_artemis123(art_fname, preload=True)
```

**Verification:**
```python
assert_array_less(amps, 1e-11)
```

### Step 12: Assign unknown = _calculate_chpi_coil_locs(...)

```python
times, cHPI_digs = _calculate_chpi_coil_locs(raw, verbose='debug')
```

**Verification:**
```python
assert_array_less(1e-13, amps)
```

### Step 13: Call assert_allclose()

```python
assert_allclose(times[5], 1.5, atol=0.2)
```

**Verification:**
```python
assert chpi_locs['rrs'].shape == (0, 3, 3)
```

### Step 14: Call assert_allclose()

```python
assert_allclose(cHPI_digs[5][0]['gof'], 0.995, atol=0.005)
```

**Verification:**
```python
assert pos.shape == (0, 10)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(cHPI_digs[5][0]['r'], [-0.0157, 0.0655, 0.0018], atol=0.001)
```

### Step 16: Call _check_dists()

```python
_check_dists(raw.info, cHPI_digs[5])
```

### Step 17: Assign coil_amplitudes = compute_chpi_amplitudes(...)

```python
coil_amplitudes = compute_chpi_amplitudes(raw)
```

### Step 18: Assign amps = np.linalg.norm(...)

```python
amps = np.linalg.norm(coil_amplitudes['slopes'], axis=-1)
```

**Verification:**
```python
assert amps.shape == (len(coil_amplitudes['times']), 3)
```

### Step 19: Call assert_array_less()

```python
assert_array_less(amps, 1e-11)
```

### Step 20: Call assert_array_less()

```python
assert_array_less(1e-13, amps)
```

### Step 21: Call unknown.fill()

```python
coil_amplitudes['slopes'].fill(np.nan)
```

### Step 22: Assign chpi_locs = compute_chpi_locs(...)

```python
chpi_locs = compute_chpi_locs(raw.info, coil_amplitudes)
```

**Verification:**
```python
assert chpi_locs['rrs'].shape == (0, 3, 3)
```

### Step 23: Assign pos = compute_head_pos(...)

```python
pos = compute_head_pos(raw.info, chpi_locs)
```

**Verification:**
```python
assert pos.shape == (0, 10)
```

### Step 24: Call compute_chpi_locs()

```python
compute_chpi_locs(raw.info, coil_amplitudes, too_close='foo')
```


## Complete Example

```python
# Workflow
'Test computing just cHPI locations.'
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes', preload=True)
raw_dec = _decimate_chpi(raw, 15)
times, cHPI_digs = _calculate_chpi_coil_locs(raw_dec, verbose='debug')
assert_allclose(times[0], 9.0, atol=0.01)
assert_allclose(cHPI_digs[0][2]['r'], [-0.01937833, 0.00346804, 0.06331209], atol=0.001)
assert_allclose(cHPI_digs[0][2]['gof'], 0.9957, atol=0.001)
assert_allclose(cHPI_digs[0][4]['r'], [-0.0655, 0.0755, 0.0004], atol=0.003)
assert_allclose(cHPI_digs[0][4]['gof'], 0.9323, atol=0.001)
_check_dists(raw.info, cHPI_digs[0], n_bad=1)
raw = read_raw_artemis123(art_fname, preload=True)
times, cHPI_digs = _calculate_chpi_coil_locs(raw, verbose='debug')
assert len(np.setdiff1d(times, raw.times + raw.first_time)) == 0
assert_allclose(times[5], 1.5, atol=0.2)
assert_allclose(cHPI_digs[5][0]['gof'], 0.995, atol=0.005)
assert_allclose(cHPI_digs[5][0]['r'], [-0.0157, 0.0655, 0.0018], atol=0.001)
_check_dists(raw.info, cHPI_digs[5])
coil_amplitudes = compute_chpi_amplitudes(raw)
with pytest.raises(ValueError, match='too_close'):
    compute_chpi_locs(raw.info, coil_amplitudes, too_close='foo')
amps = np.linalg.norm(coil_amplitudes['slopes'], axis=-1)
amps /= coil_amplitudes['slopes'].shape[-1]
assert amps.shape == (len(coil_amplitudes['times']), 3)
assert_array_less(amps, 1e-11)
assert_array_less(1e-13, amps)
coil_amplitudes['slopes'].fill(np.nan)
chpi_locs = compute_chpi_locs(raw.info, coil_amplitudes)
assert chpi_locs['rrs'].shape == (0, 3, 3)
pos = compute_head_pos(raw.info, chpi_locs)
assert pos.shape == (0, 10)
```

## Next Steps


---

*Source: test_chpi.py:630 | Complexity: Advanced | Last updated: 2026-05-18*