# How To: Fidsposition Information

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test reading file with 3 fiducial locations.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `time`
- `copy`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne.annotations`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.io.eeglab._eeglab`
- `mne.io.eeglab.eeglab`
- `mne.io.tests.test_raw`
- `mne.utils`
- `eeglabio.raw`

**Setup Required:**
```python
# Fixtures: monkeypatch, has_type
```

## Step-by-Step Guide

### Step 1: 'Test reading file with 3 fiducial locations.'

```python
'Test reading file with 3 fiducial locations.'
```

**Verification:**
```python
assert_allclose(pos['nasion'], [0, 0.0997, 0], atol=0.0001)
```

### Step 2: Assign raw = read_raw_eeglab(...)

```python
raw = read_raw_eeglab(raw_fname_chanloc_fids, montage_units='cm')
```

**Verification:**
```python
assert_allclose(pos['lpa'], -pos['nasion'][[1, 0, 0]])
```

### Step 3: Assign montage = raw.get_montage(...)

```python
montage = raw.get_montage()
```

**Verification:**
```python
assert_allclose(pos['rpa'], pos['nasion'][[1, 0, 0]])
```

### Step 4: Assign pos = montage.get_positions(...)

```python
pos = montage.get_positions()
```

**Verification:**
```python
assert pos['nasion'] is not None
```

### Step 5: Assign n_eeg = 129

```python
n_eeg = 129
```

**Verification:**
```python
assert pos['lpa'] is not None
```

### Step 6: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne.io.eeglab.eeglab, '_get_montage_information', get_bad_information)
```

**Verification:**
```python
assert pos['rpa'] is not None
```

### Step 7: Call assert_allclose()

```python
assert_allclose(pos['nasion'], [0, 0.0997, 0], atol=0.0001)
```

**Verification:**
```python
assert len(pos['nasion']) == 3
```

### Step 8: Call assert_allclose()

```python
assert_allclose(pos['lpa'], -pos['nasion'][[1, 0, 0]])
```

**Verification:**
```python
assert len(pos['lpa']) == 3
```

### Step 9: Call assert_allclose()

```python
assert_allclose(pos['rpa'], pos['nasion'][[1, 0, 0]])
```

**Verification:**
```python
assert len(pos['rpa']) == 3
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch, has_type

# Workflow
'Test reading file with 3 fiducial locations.'
if not has_type:

    def get_bad_information(eeg, get_pos, *, montage_units):
        del eeg.chaninfo['nodatchans']['type']
        return _get_montage_information(eeg, get_pos, montage_units=montage_units)
    monkeypatch.setattr(mne.io.eeglab.eeglab, '_get_montage_information', get_bad_information)
raw = read_raw_eeglab(raw_fname_chanloc_fids, montage_units='cm')
montage = raw.get_montage()
pos = montage.get_positions()
n_eeg = 129
if not has_type:
    assert_allclose(pos['nasion'], [0, 0.0997, 0], atol=0.0001)
    assert_allclose(pos['lpa'], -pos['nasion'][[1, 0, 0]])
    assert_allclose(pos['rpa'], pos['nasion'][[1, 0, 0]])
assert pos['nasion'] is not None
assert pos['lpa'] is not None
assert pos['rpa'] is not None
assert len(pos['nasion']) == 3
assert len(pos['lpa']) == 3
assert len(pos['rpa']) == 3
assert len(raw.info['dig']) == n_eeg + 3
```

## Next Steps


---

*Source: test_eeglab.py:709 | Complexity: Advanced | Last updated: 2026-05-18*