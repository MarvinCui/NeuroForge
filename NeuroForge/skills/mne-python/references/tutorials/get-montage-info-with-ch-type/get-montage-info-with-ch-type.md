# How To: Get Montage Info With Ch Type

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that the channel types are properly returned.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test that the channel types are properly returned.'

```python
'Test that the channel types are properly returned.'
```

**Verification:**
```python
assert len(ch_names) == len(ch_types) == n
```

### Step 2: Assign mat = _readmat(...)

```python
mat = _readmat(raw_fname_onefile_mat)
```

**Verification:**
```python
assert ch_types == ['eeg'] * (n - 2) + ['eog'] + ['stim']
```

### Step 3: Assign n = len(...)

```python
n = len(mat['EEG']['chanlocs']['labels'])
```

**Verification:**
```python
assert montage is None
```

### Step 4: Assign unknown = value

```python
mat['EEG']['chanlocs']['type'] = ['eeg'] * (n - 2) + ['eog'] + ['stim']
```

### Step 5: Assign unknown = _dol_to_lod(...)

```python
mat['EEG']['chanlocs'] = _dol_to_lod(mat['EEG']['chanlocs'])
```

### Step 6: Assign unknown = Bunch(...)

```python
mat['EEG'] = Bunch(**mat['EEG'])
```

### Step 7: Assign unknown = _get_montage_information(...)

```python
ch_names, ch_types, montage = _get_montage_information(mat['EEG'], get_pos=False, montage_units='mm')
```

**Verification:**
```python
assert len(ch_names) == len(ch_types) == n
```

### Step 8: Assign mat = _readmat(...)

```python
mat = _readmat(raw_fname_onefile_mat)
```

### Step 9: Assign n = len(...)

```python
n = len(mat['EEG']['chanlocs']['labels'])
```

### Step 10: Assign unknown = value

```python
mat['EEG']['chanlocs']['type'] = ['eeg'] * (n - 2) + ['eog'] + ['unknown']
```

### Step 11: Assign unknown = _dol_to_lod(...)

```python
mat['EEG']['chanlocs'] = _dol_to_lod(mat['EEG']['chanlocs'])
```

### Step 12: Assign unknown = Bunch(...)

```python
mat['EEG'] = Bunch(**mat['EEG'])
```

### Step 13: Assign unknown = _get_montage_information(...)

```python
ch_names, ch_types, montage = _get_montage_information(mat['EEG'], get_pos=False, montage_units='mm')
```


## Complete Example

```python
# Workflow
'Test that the channel types are properly returned.'
mat = _readmat(raw_fname_onefile_mat)
n = len(mat['EEG']['chanlocs']['labels'])
mat['EEG']['chanlocs']['type'] = ['eeg'] * (n - 2) + ['eog'] + ['stim']
mat['EEG']['chanlocs'] = _dol_to_lod(mat['EEG']['chanlocs'])
mat['EEG'] = Bunch(**mat['EEG'])
ch_names, ch_types, montage = _get_montage_information(mat['EEG'], get_pos=False, montage_units='mm')
assert len(ch_names) == len(ch_types) == n
assert ch_types == ['eeg'] * (n - 2) + ['eog'] + ['stim']
assert montage is None
mat = _readmat(raw_fname_onefile_mat)
n = len(mat['EEG']['chanlocs']['labels'])
mat['EEG']['chanlocs']['type'] = ['eeg'] * (n - 2) + ['eog'] + ['unknown']
mat['EEG']['chanlocs'] = _dol_to_lod(mat['EEG']['chanlocs'])
mat['EEG'] = Bunch(**mat['EEG'])
with pytest.warns(RuntimeWarning, match='Unknown types found'):
    ch_names, ch_types, montage = _get_montage_information(mat['EEG'], get_pos=False, montage_units='mm')
```

## Next Steps


---

*Source: test_eeglab.py:677 | Complexity: Advanced | Last updated: 2026-05-18*