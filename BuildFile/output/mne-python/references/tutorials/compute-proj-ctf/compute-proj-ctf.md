# How To: Compute Proj Ctf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test to show that projector code completes on CTF data.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.proj`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing.ssp`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test to show that projector code completes on CTF data.'

```python
'Test to show that projector code completes on CTF data.'
```

**Verification:**
```python
assert len(projs) == 5 + n_projs_init
```

### Step 2: Assign raw = read_raw_ctf(...)

```python
raw = read_raw_ctf(ctf_fname, preload=True)
```

**Verification:**
```python
assert len(projs) == 4 + n_projs_init
```

### Step 3: Assign mag_picks = value

```python
mag_picks = pick_types(raw.info, meg='mag', ref_meg=False, exclude='bads')[::10]
```

### Step 4: Assign n_mags = len(...)

```python
n_mags = len(mag_picks)
```

### Step 5: Assign grad_picks = value

```python
grad_picks = pick_types(raw.info, meg='grad', ref_meg=False, exclude='bads')[::10]
```

### Step 6: Assign n_grads = len(...)

```python
n_grads = len(grad_picks)
```

### Step 7: Assign eeg_picks = value

```python
eeg_picks = pick_types(raw.info, meg=False, eeg=True, ref_meg=False, exclude='bads')[2::3]
```

### Step 8: Assign n_eegs = len(...)

```python
n_eegs = len(eeg_picks)
```

### Step 9: Assign ref_picks = pick_types(...)

```python
ref_picks = pick_types(raw.info, meg=False, ref_meg=True)
```

### Step 10: Call raw.pick()

```python
raw.pick(np.sort(np.concatenate([mag_picks, grad_picks, eeg_picks, ref_picks])))
```

### Step 11: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(0)
```

### Step 12: Assign n_projs_init = len(...)

```python
n_projs_init = len(raw.info['projs'])
```

### Step 13: Call _check_projs_for_expected_channels()

```python
_check_projs_for_expected_channels(projs, n_mags, n_grads, n_eegs)
```

**Verification:**
```python
assert len(projs) == 5 + n_projs_init
```

### Step 14: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(1)
```

### Step 15: Call _check_projs_for_expected_channels()

```python
_check_projs_for_expected_channels(projs, n_mags, n_grads, n_eegs)
```

**Verification:**
```python
assert len(projs) == 4 + n_projs_init
```

### Step 16: Assign unknown = compute_proj_eog(...)

```python
projs, _ = compute_proj_eog(raw, n_mag=2, n_grad=2, n_eeg=2, average=True, ch_name='EEG059', avg_ref=True, no_proj=False, l_freq=None, h_freq=None, reject=None, tmax=dur_use, filter_length=1000)
```

### Step 17: Assign unknown = compute_proj_ecg(...)

```python
projs, _ = compute_proj_ecg(raw, n_mag=1, n_grad=1, n_eeg=2, average=True, ch_name='EEG059', avg_ref=True, no_proj=False, l_freq=None, h_freq=None, reject=None, tmax=dur_use, filter_length=1000)
```


## Complete Example

```python
# Workflow
'Test to show that projector code completes on CTF data.'
raw = read_raw_ctf(ctf_fname, preload=True)
mag_picks = pick_types(raw.info, meg='mag', ref_meg=False, exclude='bads')[::10]
n_mags = len(mag_picks)
grad_picks = pick_types(raw.info, meg='grad', ref_meg=False, exclude='bads')[::10]
n_grads = len(grad_picks)
eeg_picks = pick_types(raw.info, meg=False, eeg=True, ref_meg=False, exclude='bads')[2::3]
n_eegs = len(eeg_picks)
ref_picks = pick_types(raw.info, meg=False, ref_meg=True)
raw.pick(np.sort(np.concatenate([mag_picks, grad_picks, eeg_picks, ref_picks])))
del mag_picks, grad_picks, eeg_picks, ref_picks
raw.apply_gradient_compensation(0)
n_projs_init = len(raw.info['projs'])
with pytest.warns(RuntimeWarning, match='Attenuation'):
    projs, _ = compute_proj_eog(raw, n_mag=2, n_grad=2, n_eeg=2, average=True, ch_name='EEG059', avg_ref=True, no_proj=False, l_freq=None, h_freq=None, reject=None, tmax=dur_use, filter_length=1000)
_check_projs_for_expected_channels(projs, n_mags, n_grads, n_eegs)
assert len(projs) == 5 + n_projs_init
raw.apply_gradient_compensation(1)
with pytest.warns(RuntimeWarning, match='Attenuation'):
    projs, _ = compute_proj_ecg(raw, n_mag=1, n_grad=1, n_eeg=2, average=True, ch_name='EEG059', avg_ref=True, no_proj=False, l_freq=None, h_freq=None, reject=None, tmax=dur_use, filter_length=1000)
_check_projs_for_expected_channels(projs, n_mags, n_grads, n_eegs)
assert len(projs) == 4 + n_projs_init
```

## Next Steps


---

*Source: test_ssp.py:219 | Complexity: Advanced | Last updated: 2026-05-18*