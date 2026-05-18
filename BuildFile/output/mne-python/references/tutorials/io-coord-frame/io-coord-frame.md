# How To: Io Coord Frame

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test round trip for coordinate frame.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `pickle`
- `string`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.proj`
- `mne._fiff.tag`
- `mne._fiff.write`
- `mne.channels`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.minimum_norm`
- `mne.transforms`
- `mne.utils`
- `mne.utils._bunch`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test round trip for coordinate frame.'

```python
'Test round trip for coordinate frame.'
```

**Verification:**
```python
assert info2['chs'][0]['coord_frame'] == FIFF.FIFFV_COORD_HEAD
```

### Step 2: Assign fname = value

```python
fname = tmp_path / 'test.fif'
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(ch_names=['Test Ch'], sfreq=1000.0, ch_types=[ch_type])
```

### Step 4: Assign unknown = value

```python
info['chs'][0]['loc'][:3] = [0.05, 0.01, -0.03]
```

### Step 5: Call write_info()

```python
write_info(fname, info, overwrite=True)
```

### Step 6: Assign info2 = read_info(...)

```python
info2 = read_info(fname)
```

**Verification:**
```python
assert info2['chs'][0]['coord_frame'] == FIFF.FIFFV_COORD_HEAD
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test round trip for coordinate frame.'
fname = tmp_path / 'test.fif'
for ch_type in ('eeg', 'seeg', 'ecog', 'dbs', 'hbo', 'hbr'):
    info = create_info(ch_names=['Test Ch'], sfreq=1000.0, ch_types=[ch_type])
    info['chs'][0]['loc'][:3] = [0.05, 0.01, -0.03]
    write_info(fname, info, overwrite=True)
    info2 = read_info(fname)
    assert info2['chs'][0]['coord_frame'] == FIFF.FIFFV_COORD_HEAD
```

## Next Steps


---

*Source: test_meas_info.py:507 | Complexity: Intermediate | Last updated: 2026-05-18*