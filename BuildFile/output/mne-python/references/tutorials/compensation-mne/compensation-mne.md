# How To: Compensation Mne

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test comensation by comparing with MNE.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.compensator`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test comensation by comparing with MNE.'

```python
'Test comensation by comparing with MNE.'
```

**Verification:**
```python
assert_allclose(evoked_py.data[picks_py], evoked_c.data[picks_c], rtol=0.001, atol=1e-17)
```

### Step 2: Assign fname_default = value

```python
fname_default = tmp_path / 'ctf_default-ave.fif'
```

**Verification:**
```python
assert ch_py['coil_type'] == ch_c['coil_type']
```

### Step 3: Call make_evoked.save()

```python
make_evoked(ctf_comp_fname, None).save(fname_default)
```

### Step 4: """Make evoked data."""

```python
"""Make evoked data."""
```

### Step 5: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname)
```

### Step 6: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=True, ref_meg=True)
```

### Step 7: Assign events = np.array(...)

```python
events = np.array([[0, 0, 1]], dtype=np.int64)
```

### Step 8: Assign evoked = Epochs.average(...)

```python
evoked = Epochs(raw, events, 1, 0, 0.02, picks=picks, baseline=None).average()
```

### Step 9: """Compensate using MNE-C."""

```python
"""Compensate using MNE-C."""
```

### Step 10: Assign tmp_fname = value

```python
tmp_fname = f'{fname.stem}-{comp}-ave.fif'
```

### Step 11: Assign cmd = value

```python
cmd = ['mne_compensate_data', '--in', str(fname), '--out', tmp_fname, '--grad', str(comp)]
```

### Step 12: Call run_subprocess()

```python
run_subprocess(cmd)
```

### Step 13: Assign evoked_py = make_evoked(...)

```python
evoked_py = make_evoked(ctf_comp_fname, comp)
```

### Step 14: Assign evoked_c = compensate_mne(...)

```python
evoked_c = compensate_mne(fname_default, comp)
```

### Step 15: Assign picks_py = pick_types(...)

```python
picks_py = pick_types(evoked_py.info, meg=True, ref_meg=True)
```

### Step 16: Assign picks_c = pick_types(...)

```python
picks_c = pick_types(evoked_c.info, meg=True, ref_meg=True)
```

### Step 17: Call assert_allclose()

```python
assert_allclose(evoked_py.data[picks_py], evoked_c.data[picks_c], rtol=0.001, atol=1e-17)
```

### Step 18: Assign chs_py = value

```python
chs_py = [evoked_py.info['chs'][ii] for ii in picks_py]
```

### Step 19: Assign chs_c = value

```python
chs_c = [evoked_c.info['chs'][ii] for ii in picks_c]
```

### Step 20: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(comp)
```

**Verification:**
```python
assert ch_py['coil_type'] == ch_c['coil_type']
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test comensation by comparing with MNE.'

def make_evoked(fname, comp):
    """Make evoked data."""
    raw = read_raw_fif(fname)
    if comp is not None:
        raw.apply_gradient_compensation(comp)
    picks = pick_types(raw.info, meg=True, ref_meg=True)
    events = np.array([[0, 0, 1]], dtype=np.int64)
    evoked = Epochs(raw, events, 1, 0, 0.02, picks=picks, baseline=None).average()
    return evoked

def compensate_mne(fname, comp):
    """Compensate using MNE-C."""
    tmp_fname = f'{fname.stem}-{comp}-ave.fif'
    cmd = ['mne_compensate_data', '--in', str(fname), '--out', tmp_fname, '--grad', str(comp)]
    run_subprocess(cmd)
    return read_evokeds(tmp_fname)[0]
fname_default = tmp_path / 'ctf_default-ave.fif'
make_evoked(ctf_comp_fname, None).save(fname_default)
for comp in [0, 1, 2, 3]:
    evoked_py = make_evoked(ctf_comp_fname, comp)
    evoked_c = compensate_mne(fname_default, comp)
    picks_py = pick_types(evoked_py.info, meg=True, ref_meg=True)
    picks_c = pick_types(evoked_c.info, meg=True, ref_meg=True)
    assert_allclose(evoked_py.data[picks_py], evoked_c.data[picks_c], rtol=0.001, atol=1e-17)
    chs_py = [evoked_py.info['chs'][ii] for ii in picks_py]
    chs_c = [evoked_c.info['chs'][ii] for ii in picks_c]
    for ch_py, ch_c in zip(chs_py, chs_c):
        assert ch_py['coil_type'] == ch_c['coil_type']
```

## Next Steps


---

*Source: test_compensator.py:75 | Complexity: Advanced | Last updated: 2026-05-18*