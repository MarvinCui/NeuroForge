# How To: Coreg Class Init

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that Coregistration can be instantiated with various digs.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `functools`
- `glob`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.source_space`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: drop_point_kind
```

## Step-by-Step Guide

### Step 1: 'Test that Coregistration can be instantiated with various digs.'

```python
'Test that Coregistration can be instantiated with various digs.'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

### Step 3: Assign unknown = read_fiducials(...)

```python
fiducials, _ = read_fiducials(fid_fname)
```

### Step 4: Assign info = read_info(...)

```python
info = read_info(raw_fname)
```

### Step 5: Assign dig_list = value

```python
dig_list = []
```

### Step 6: Assign eeg_chans = value

```python
eeg_chans = []
```

### Step 7: Assign this_info = info.copy(...)

```python
this_info = info.copy()
```

### Step 8: Call this_info.set_montage()

```python
this_info.set_montage(DigMontage(dig=dig_list, ch_names=eeg_chans), on_missing='ignore')
```

### Step 9: Call Coregistration()

```python
Coregistration(this_info, subject='sample', subjects_dir=subjects_dir, fiducials=fiducials)
```

### Step 10: Call dig_list.append()

```python
dig_list.append(pt)
```

### Step 11: Call eeg_chans.append()

```python
eeg_chans.append(f"EEG {pt['ident']:03d}")
```


## Complete Example

```python
# Setup
# Fixtures: drop_point_kind

# Workflow
'Test that Coregistration can be instantiated with various digs.'
pytest.importorskip('nibabel')
fiducials, _ = read_fiducials(fid_fname)
info = read_info(raw_fname)
dig_list = []
eeg_chans = []
for pt in info['dig']:
    if pt['kind'] != drop_point_kind:
        dig_list.append(pt)
        if pt['kind'] == FIFF.FIFFV_POINT_EEG:
            eeg_chans.append(f"EEG {pt['ident']:03d}")
this_info = info.copy()
this_info.set_montage(DigMontage(dig=dig_list, ch_names=eeg_chans), on_missing='ignore')
Coregistration(this_info, subject='sample', subjects_dir=subjects_dir, fiducials=fiducials)
```

## Next Steps


---

*Source: test_coreg.py:590 | Complexity: Advanced | Last updated: 2026-05-18*