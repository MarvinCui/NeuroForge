# How To: Clean Info Bads

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test cleaning info['bads'] when bad_channels are excluded.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`


## Step-by-Step Guide

### Step 1: "Test cleaning info['bads'] when bad_channels are excluded."

```python
"Test cleaning info['bads'] when bad_channels are excluded."
```

**Verification:**
```python
assert len(raw.info['projs']) == 3
```

### Step 2: Assign raw_file = value

```python
raw_file = io_dir / 'tests' / 'data' / 'test_raw.fif'
```

**Verification:**
```python
assert len(raw.info['projs']) == 4
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_file)
```

**Verification:**
```python
assert len(info_eeg['projs']) == 1
```

### Step 4: Call _assert_channel_types()

```python
_assert_channel_types(raw.info)
```

**Verification:**
```python
assert len(info_meg['projs']) == 3
```

### Step 5: Assign picks_eeg = pick_types(...)

```python
picks_eeg = pick_types(raw.info, meg=False, eeg=True)
```

**Verification:**
```python
assert info_eeg['bads'] == eeg_bad_ch
```

### Step 6: Assign idx_eeg_bad_ch = value

```python
idx_eeg_bad_ch = picks_eeg[[1, 5, 14]]
```

**Verification:**
```python
assert info_meg['bads'] == meg_bad_ch
```

### Step 7: Assign eeg_bad_ch = value

```python
eeg_bad_ch = [raw.info['ch_names'][k] for k in idx_eeg_bad_ch]
```

### Step 8: Assign picks_meg = pick_types(...)

```python
picks_meg = pick_types(raw.info, meg=True, eeg=False)
```

### Step 9: Assign idx_meg_bad_ch = value

```python
idx_meg_bad_ch = picks_meg[[0, 15, 34]]
```

### Step 10: Assign meg_bad_ch = value

```python
meg_bad_ch = [raw.info['ch_names'][k] for k in idx_meg_bad_ch]
```

### Step 11: Assign unknown = value

```python
raw.info['bads'] = eeg_bad_ch + meg_bad_ch
```

**Verification:**
```python
assert len(raw.info['projs']) == 3
```

### Step 12: Call raw.set_eeg_reference()

```python
raw.set_eeg_reference(projection=True)
```

**Verification:**
```python
assert len(raw.info['projs']) == 4
```

### Step 13: Assign info_eeg = pick_info(...)

```python
info_eeg = pick_info(raw.info, picks_eeg)
```

**Verification:**
```python
assert len(info_eeg['projs']) == 1
```

### Step 14: Assign info_meg = pick_info(...)

```python
info_meg = pick_info(raw.info, picks_meg)
```

**Verification:**
```python
assert len(info_meg['projs']) == 3
```

### Step 15: Assign info = pick_info(...)

```python
info = pick_info(raw.info, picks_meg)
```

### Step 16: Call info._check_consistency()

```python
info._check_consistency()
```

### Step 17: Call pick_info()

```python
pick_info(raw.info, [0, 0])
```


## Complete Example

```python
# Workflow
"Test cleaning info['bads'] when bad_channels are excluded."
raw_file = io_dir / 'tests' / 'data' / 'test_raw.fif'
raw = read_raw_fif(raw_file)
_assert_channel_types(raw.info)
picks_eeg = pick_types(raw.info, meg=False, eeg=True)
idx_eeg_bad_ch = picks_eeg[[1, 5, 14]]
eeg_bad_ch = [raw.info['ch_names'][k] for k in idx_eeg_bad_ch]
picks_meg = pick_types(raw.info, meg=True, eeg=False)
idx_meg_bad_ch = picks_meg[[0, 15, 34]]
meg_bad_ch = [raw.info['ch_names'][k] for k in idx_meg_bad_ch]
raw.info['bads'] = eeg_bad_ch + meg_bad_ch
assert len(raw.info['projs']) == 3
raw.set_eeg_reference(projection=True)
assert len(raw.info['projs']) == 4
info_eeg = pick_info(raw.info, picks_eeg)
assert len(info_eeg['projs']) == 1
info_meg = pick_info(raw.info, picks_meg)
assert len(info_meg['projs']) == 3
assert info_eeg['bads'] == eeg_bad_ch
assert info_meg['bads'] == meg_bad_ch
info = pick_info(raw.info, picks_meg)
info._check_consistency()
with pytest.raises(ValueError, match='do not exist'):
    info['bads'] += ['EEG 053']
with pytest.raises(ValueError, match='unique'):
    pick_info(raw.info, [0, 0])
```

## Next Steps


---

*Source: test_pick.py:539 | Complexity: Advanced | Last updated: 2026-05-18*