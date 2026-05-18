# How To: Simulate Raw Chpi

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test simulation of raw data with cHPI.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.chpi`
- `mne.datasets`
- `mne.io`
- `mne.label`
- `mne.simulation`
- `mne.simulation.source`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.tests.test_chpi`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test simulation of raw data with cHPI.'

```python
'Test simulation of raw data with cHPI.'
```

**Verification:**
```python
assert_allclose(raw_sim[hpi_pick][0], 0.0)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_chpi_fname, allow_maxshield='yes')
```

**Verification:**
```python
assert_allclose(raw_chpi[hpi_pick][0], hpi_ons.sum())
```

### Step 3: Assign drops = value

```python
drops = pick_types(raw.info, meg=True, eeg=True)[::4]
```

**Verification:**
```python
assert_array_equal(freqs_sim, freqs_chpi)
```

### Step 4: Assign picks = np.setdiff1d(...)

```python
picks = np.setdiff1d(range(len(raw.ch_names)), drops)
```

**Verification:**
```python
assert (psd_chpi[:, freq_idx] > 100 * psd_sim[:, freq_idx]).all()
```

### Step 5: Call raw.pick.load_data()

```python
raw.pick(picks).load_data()
```

**Verification:**
```python
assert_allclose(psd_sim, psd_chpi, atol=1e-20)
```

### Step 6: Call raw.info.normalize_proj()

```python
raw.info.normalize_proj()
```

### Step 7: Assign sphere = make_sphere_model(...)

```python
sphere = make_sphere_model('auto', 'auto', raw.info)
```

### Step 8: Assign sphere_vol = value

```python
sphere_vol = tuple(sphere['r0']) + (sphere.radius,)
```

### Step 9: Assign src = setup_volume_source_space(...)

```python
src = setup_volume_source_space(sphere=sphere_vol, pos=70.0, sphere_units='m')
```

### Step 10: Assign stcs = value

```python
stcs = [_make_stc(raw, src)] * 15
```

### Step 11: Assign raw_sim = simulate_raw(...)

```python
raw_sim = simulate_raw(raw.info, stc=stcs, trans=None, src=src, bem=sphere, head_pos=pos_fname, interp='zero', first_samp=raw.first_samp)
```

### Step 12: Assign raw_chpi = add_chpi(...)

```python
raw_chpi = add_chpi(raw_sim.copy(), head_pos=pos_fname, interp='zero')
```

### Step 13: Assign unknown = get_chpi_info(...)

```python
hpi_freqs, hpi_pick, hpi_ons = get_chpi_info(raw.info, on_missing='raise')
```

### Step 14: Call assert_allclose()

```python
assert_allclose(raw_sim[hpi_pick][0], 0.0)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(raw_chpi[hpi_pick][0], hpi_ons.sum())
```

### Step 16: Assign picks_meg = value

```python
picks_meg = pick_types(raw.info, meg=True)[:3]
```

### Step 17: Assign picks_eeg = value

```python
picks_eeg = pick_types(raw.info, eeg=True)[:3]
```

### Step 18: Assign chpi_amplitudes = compute_chpi_amplitudes(...)

```python
chpi_amplitudes = compute_chpi_amplitudes(raw, t_step_min=10.0)
```

### Step 19: Assign coil_locs = compute_chpi_locs(...)

```python
coil_locs = compute_chpi_locs(raw.info, chpi_amplitudes)
```

### Step 20: Assign quats_sim = compute_head_pos(...)

```python
quats_sim = compute_head_pos(raw_chpi.info, coil_locs)
```

### Step 21: Assign quats = read_head_pos(...)

```python
quats = read_head_pos(pos_fname)
```

### Step 22: Call _assert_quats()

```python
_assert_quats(quats, quats_sim, dist_tol=0.005, angle_tol=3.5, vel_atol=0.03)
```

### Step 23: Assign unknown = raw_sim.compute_psd.get_data(...)

```python
psd_sim, freqs_sim = raw_sim.compute_psd(picks=picks).get_data(return_freqs=True)
```

### Step 24: Assign unknown = raw_chpi.compute_psd.get_data(...)

```python
psd_chpi, freqs_chpi = raw_chpi.compute_psd(picks=picks).get_data(return_freqs=True)
```

### Step 25: Call assert_array_equal()

```python
assert_array_equal(freqs_sim, freqs_chpi)
```

### Step 26: Assign freq_idx = np.argmin(...)

```python
freq_idx = np.argmin(np.abs(freqs_sim - hpi_freqs[:, np.newaxis]), axis=1)
```

**Verification:**
```python
assert (psd_chpi[:, freq_idx] > 100 * psd_sim[:, freq_idx]).all()
```

### Step 27: Call assert_allclose()

```python
assert_allclose(psd_sim, psd_chpi, atol=1e-20)
```


## Complete Example

```python
# Workflow
'Test simulation of raw data with cHPI.'
raw = read_raw_fif(raw_chpi_fname, allow_maxshield='yes')
drops = pick_types(raw.info, meg=True, eeg=True)[::4]
picks = np.setdiff1d(range(len(raw.ch_names)), drops)
raw.pick(picks).load_data()
raw.info.normalize_proj()
sphere = make_sphere_model('auto', 'auto', raw.info)
sphere_vol = tuple(sphere['r0']) + (sphere.radius,)
src = setup_volume_source_space(sphere=sphere_vol, pos=70.0, sphere_units='m')
stcs = [_make_stc(raw, src)] * 15
raw_sim = simulate_raw(raw.info, stc=stcs, trans=None, src=src, bem=sphere, head_pos=pos_fname, interp='zero', first_samp=raw.first_samp)
raw_chpi = add_chpi(raw_sim.copy(), head_pos=pos_fname, interp='zero')
hpi_freqs, hpi_pick, hpi_ons = get_chpi_info(raw.info, on_missing='raise')
assert_allclose(raw_sim[hpi_pick][0], 0.0)
assert_allclose(raw_chpi[hpi_pick][0], hpi_ons.sum())
picks_meg = pick_types(raw.info, meg=True)[:3]
picks_eeg = pick_types(raw.info, eeg=True)[:3]
for picks in (picks_meg, picks_eeg):
    psd_sim, freqs_sim = raw_sim.compute_psd(picks=picks).get_data(return_freqs=True)
    psd_chpi, freqs_chpi = raw_chpi.compute_psd(picks=picks).get_data(return_freqs=True)
    assert_array_equal(freqs_sim, freqs_chpi)
    if picks is picks_meg:
        freq_idx = np.argmin(np.abs(freqs_sim - hpi_freqs[:, np.newaxis]), axis=1)
        assert (psd_chpi[:, freq_idx] > 100 * psd_sim[:, freq_idx]).all()
    else:
        assert_allclose(psd_sim, psd_chpi, atol=1e-20)
chpi_amplitudes = compute_chpi_amplitudes(raw, t_step_min=10.0)
coil_locs = compute_chpi_locs(raw.info, chpi_amplitudes)
quats_sim = compute_head_pos(raw_chpi.info, coil_locs)
quats = read_head_pos(pos_fname)
_assert_quats(quats, quats_sim, dist_tol=0.005, angle_tol=3.5, vel_atol=0.03)
```

## Next Steps


---

*Source: test_raw.py:525 | Complexity: Advanced | Last updated: 2026-05-18*