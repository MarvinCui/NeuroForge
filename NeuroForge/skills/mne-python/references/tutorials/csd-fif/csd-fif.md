# How To: Csd Fif

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test applying CSD to FIF data.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `scipy.io`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test applying CSD to FIF data.'

```python
'Test applying CSD to FIF data.'
```

**Verification:**
```python
assert 'csd' not in raw
```

### Step 2: Assign raw = read_raw_fif.load_data(...)

```python
raw = read_raw_fif(raw_fname).load_data()
```

**Verification:**
```python
assert len(orig_eeg) == 60
```

### Step 3: Assign unknown = value

```python
raw.info['bads'] = []
```

**Verification:**
```python
assert 'eeg' not in raw_csd
```

### Step 4: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=False, eeg=True)
```

**Verification:**
```python
assert not (orig_eeg == new_eeg).any()
```

### Step 5: Assign orig_eeg = raw.get_data(...)

```python
orig_eeg = raw.get_data('eeg')
```

**Verification:**
```python
assert raw_csd.info['custom_ref_applied'] == FIFF.FIFFV_MNE_CUSTOM_REF_CSD
```

### Step 6: Assign raw_csd = compute_current_source_density(...)

```python
raw_csd = compute_current_source_density(raw)
```

**Verification:**
```python
assert ch['coil_type'] == FIFF.FIFFV_COIL_EEG_CSD
```

### Step 7: Assign new_eeg = raw_csd.get_data(...)

```python
new_eeg = raw_csd.get_data('csd')
```

**Verification:**
```python
assert ch['unit'] == FIFF.FIFF_UNIT_V_M2
```

### Step 8: Assign unknown = 0

```python
raw_csd.info['custom_ref_applied'] = 0
```

**Verification:**
```python
assert object_diff(raw.info, raw_csd.info) == ''
```

### Step 9: Assign ch = value

```python
ch = raw_csd.info['chs'][pick]
```

**Verification:**
```python
assert ch['coil_type'] == FIFF.FIFFV_COIL_EEG_CSD
```

### Step 10: Call ch.update()

```python
ch.update(coil_type=FIFF.FIFFV_COIL_EEG, unit=FIFF.FIFF_UNIT_V)
```

### Step 11: Assign unknown = value

```python
raw_csd._data[pick] = raw._data[pick]
```


## Complete Example

```python
# Workflow
'Test applying CSD to FIF data.'
raw = read_raw_fif(raw_fname).load_data()
raw.info['bads'] = []
picks = pick_types(raw.info, meg=False, eeg=True)
assert 'csd' not in raw
orig_eeg = raw.get_data('eeg')
assert len(orig_eeg) == 60
raw_csd = compute_current_source_density(raw)
assert 'eeg' not in raw_csd
new_eeg = raw_csd.get_data('csd')
assert not (orig_eeg == new_eeg).any()
assert raw_csd.info['custom_ref_applied'] == FIFF.FIFFV_MNE_CUSTOM_REF_CSD
with raw_csd.info._unlock():
    raw_csd.info['custom_ref_applied'] = 0
for pick in picks:
    ch = raw_csd.info['chs'][pick]
    assert ch['coil_type'] == FIFF.FIFFV_COIL_EEG_CSD
    assert ch['unit'] == FIFF.FIFF_UNIT_V_M2
    ch.update(coil_type=FIFF.FIFFV_COIL_EEG, unit=FIFF.FIFF_UNIT_V)
    raw_csd._data[pick] = raw._data[pick]
assert object_diff(raw.info, raw_csd.info) == ''
```

## Next Steps


---

*Source: test_csd.py:164 | Complexity: Advanced | Last updated: 2026-05-18*