# How To: Set Dig Montage

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test setting DigMontage with toy understandable points.

## Prerequisites

**Required Modules:**
- `shutil`
- `contextlib`
- `functools`
- `itertools`
- `pathlib`
- `string`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.montage`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.channels.montage`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.io.kit`
- `mne.preprocessing`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz._3d`


## Step-by-Step Guide

### Step 1: 'Test setting DigMontage with toy understandable points.'

```python
'Test setting DigMontage with toy understandable points.'
```

**Verification:**
```python
assert repr(montage_ch_only) == '<DigMontage | 0 extras (headshape), 0 HPIs, 0 fiducials, 3 channels>'
```

### Step 2: Assign unknown = value

```python
N_CHANNELS, N_HSP, N_HPI = (3, 2, 1)
```

**Verification:**
```python
assert len(info['dig']) == len(montage_ch_only.dig) + 3
```

### Step 3: Assign ch_names = list(...)

```python
ch_names = list(ascii_lowercase[:N_CHANNELS])
```

**Verification:**
```python
assert_allclose(actual=np.array([ch['loc'][:6] for ch in info['chs']]), desired=[[0.0, 1.0, 2.0, 0.0, 0.0, 0.0], [3.0, 4.0, 5.0, 0.0, 0.0, 0.0], [6.0, 7.0, 8.0, 0.0, 0.0, 0.0]])
```

### Step 4: Assign ch_pos = dict(...)

```python
ch_pos = dict(zip(ch_names, np.arange(N_CHANNELS * 3).reshape(N_CHANNELS, 3)))
```

**Verification:**
```python
assert repr(montage_full) == '<DigMontage | 2 extras (headshape), 1 HPIs, 3 fiducials, 4 channels>'
```

### Step 5: Assign montage_ch_only = make_dig_montage(...)

```python
montage_ch_only = make_dig_montage(ch_pos=ch_pos, coord_frame='head')
```

**Verification:**
```python
assert len(info['dig']) == EXPECTED_LEN
```

### Step 6: Assign info = create_info(...)

```python
info = create_info(ch_names, sfreq=1, ch_types='eeg')
```

**Verification:**
```python
assert_allclose(actual=np.array([ch['loc'][:6] for ch in info['chs']]), desired=[[0.0, 1.0, 2.0, 42.0, 42.0, 42.0], [3.0, 4.0, 5.0, 42.0, 42.0, 42.0], [6.0, 7.0, 8.0, 42.0, 42.0, 42.0]])
```

### Step 7: Call info.set_montage()

```python
info.set_montage(montage_ch_only)
```

**Verification:**
```python
assert len(info['dig']) == len(montage_ch_only.dig) + 3
```

### Step 8: Call assert_allclose()

```python
assert_allclose(actual=np.array([ch['loc'][:6] for ch in info['chs']]), desired=[[0.0, 1.0, 2.0, 0.0, 0.0, 0.0], [3.0, 4.0, 5.0, 0.0, 0.0, 0.0], [6.0, 7.0, 8.0, 0.0, 0.0, 0.0]])
```

### Step 9: Assign montage_full = make_dig_montage(...)

```python
montage_full = make_dig_montage(ch_pos=dict(**ch_pos, EEG000=np.full(3, 42)), nasion=[1, 1, 1], lpa=[2, 2, 2], rpa=[3, 3, 3], hsp=np.full((N_HSP, 3), 4), hpi=np.full((N_HPI, 3), 4), coord_frame='head')
```

**Verification:**
```python
assert repr(montage_full) == '<DigMontage | 2 extras (headshape), 1 HPIs, 3 fiducials, 4 channels>'
```

### Step 10: Assign info = create_info(...)

```python
info = create_info(ch_names, sfreq=1, ch_types='eeg')
```

### Step 11: Call info.set_montage()

```python
info.set_montage(montage_full)
```

### Step 12: Assign EXPECTED_LEN = sum(...)

```python
EXPECTED_LEN = sum({'hsp': 2, 'hpi': 1, 'fid': 3, 'eeg': 4}.values())
```

**Verification:**
```python
assert len(info['dig']) == EXPECTED_LEN
```

### Step 13: Call assert_allclose()

```python
assert_allclose(actual=np.array([ch['loc'][:6] for ch in info['chs']]), desired=[[0.0, 1.0, 2.0, 42.0, 42.0, 42.0], [3.0, 4.0, 5.0, 42.0, 42.0, 42.0], [6.0, 7.0, 8.0, 42.0, 42.0, 42.0]])
```


## Complete Example

```python
# Workflow
'Test setting DigMontage with toy understandable points.'
N_CHANNELS, N_HSP, N_HPI = (3, 2, 1)
ch_names = list(ascii_lowercase[:N_CHANNELS])
ch_pos = dict(zip(ch_names, np.arange(N_CHANNELS * 3).reshape(N_CHANNELS, 3)))
montage_ch_only = make_dig_montage(ch_pos=ch_pos, coord_frame='head')
assert repr(montage_ch_only) == '<DigMontage | 0 extras (headshape), 0 HPIs, 0 fiducials, 3 channels>'
info = create_info(ch_names, sfreq=1, ch_types='eeg')
info.set_montage(montage_ch_only)
assert len(info['dig']) == len(montage_ch_only.dig) + 3
assert_allclose(actual=np.array([ch['loc'][:6] for ch in info['chs']]), desired=[[0.0, 1.0, 2.0, 0.0, 0.0, 0.0], [3.0, 4.0, 5.0, 0.0, 0.0, 0.0], [6.0, 7.0, 8.0, 0.0, 0.0, 0.0]])
montage_full = make_dig_montage(ch_pos=dict(**ch_pos, EEG000=np.full(3, 42)), nasion=[1, 1, 1], lpa=[2, 2, 2], rpa=[3, 3, 3], hsp=np.full((N_HSP, 3), 4), hpi=np.full((N_HPI, 3), 4), coord_frame='head')
assert repr(montage_full) == '<DigMontage | 2 extras (headshape), 1 HPIs, 3 fiducials, 4 channels>'
info = create_info(ch_names, sfreq=1, ch_types='eeg')
info.set_montage(montage_full)
EXPECTED_LEN = sum({'hsp': 2, 'hpi': 1, 'fid': 3, 'eeg': 4}.values())
assert len(info['dig']) == EXPECTED_LEN
assert_allclose(actual=np.array([ch['loc'][:6] for ch in info['chs']]), desired=[[0.0, 1.0, 2.0, 42.0, 42.0, 42.0], [3.0, 4.0, 5.0, 42.0, 42.0, 42.0], [6.0, 7.0, 8.0, 42.0, 42.0, 42.0]])
```

## Next Steps


---

*Source: test_montage.py:984 | Complexity: Advanced | Last updated: 2026-05-18*