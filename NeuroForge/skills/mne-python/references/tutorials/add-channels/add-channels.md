# How To: Add Channels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test tfr splitting / re-appending channel types.

## Prerequisites

**Required Modules:**
- `datetime`
- `re`
- `itertools`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.collections`
- `numpy.testing`
- `mne`
- `mne`
- `mne.epochs`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.tfr`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz.utils`
- `test_spectrum`
- `pandas.testing`


## Step-by-Step Guide

### Step 1: 'Test tfr splitting / re-appending channel types.'

```python
'Test tfr splitting / re-appending channel types.'
```

**Verification:**
```python
assert all((ch in tfr_new.ch_names for ch in tfr_stim.ch_names + tfr_meg.ch_names))
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((6, 2, 3))
```

**Verification:**
```python
assert have_all
```

### Step 3: Assign times = np.array(...)

```python
times = np.array([0.1, 0.2, 0.3])
```

**Verification:**
```python
assert_array_equal(tfr_new.data, tfr_eeg_meg.data)
```

### Step 4: Assign freqs = np.array(...)

```python
freqs = np.array([0.1, 0.2])
```

**Verification:**
```python
assert all((ch not in tfr_new.ch_names for ch in tfr_stim.ch_names))
```

### Step 5: Assign info = mne.create_info(...)

```python
info = mne.create_info(['MEG 001', 'MEG 002', 'MEG 003', 'EEG 001', 'EEG 002', 'STIM 001'], 1000.0, ['mag', 'mag', 'mag', 'eeg', 'eeg', 'stim'])
```

**Verification:**
```python
assert tfr1.ch_names == ['EEG 001', 'EEG 002', 'EEG 003']
```

### Step 6: Assign tfr = AverageTFRArray(...)

```python
tfr = AverageTFRArray(info=info, data=data, times=times, freqs=freqs, nave=20, comment='test', method='crazy-tfr')
```

**Verification:**
```python
assert tfr1.data.shape == (5, 3, 2, 3)
```

### Step 7: Assign tfr_eeg = tfr.copy.pick(...)

```python
tfr_eeg = tfr.copy().pick(picks='eeg')
```

### Step 8: Assign tfr_meg = tfr.copy.pick(...)

```python
tfr_meg = tfr.copy().pick(picks='meg')
```

### Step 9: Assign tfr_stim = tfr.copy.pick(...)

```python
tfr_stim = tfr.copy().pick(picks='stim')
```

### Step 10: Assign tfr_eeg_meg = tfr.copy.pick(...)

```python
tfr_eeg_meg = tfr.copy().pick(picks=['meg', 'eeg'])
```

### Step 11: Assign tfr_new = tfr_meg.copy.add_channels(...)

```python
tfr_new = tfr_meg.copy().add_channels([tfr_eeg, tfr_stim])
```

**Verification:**
```python
assert all((ch in tfr_new.ch_names for ch in tfr_stim.ch_names + tfr_meg.ch_names))
```

### Step 12: Assign tfr_new = tfr_meg.copy.add_channels(...)

```python
tfr_new = tfr_meg.copy().add_channels([tfr_eeg])
```

### Step 13: Assign have_all = all(...)

```python
have_all = all((ch in tfr_new.ch_names for ch in tfr.ch_names if ch != 'STIM 001'))
```

**Verification:**
```python
assert have_all
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(tfr_new.data, tfr_eeg_meg.data)
```

**Verification:**
```python
assert all((ch not in tfr_new.ch_names for ch in tfr_stim.ch_names))
```

### Step 15: Assign tfr_badsf = tfr_eeg.copy(...)

```python
tfr_badsf = tfr_eeg.copy()
```

### Step 16: Assign tfr_eeg = tfr_eeg.crop(...)

```python
tfr_eeg = tfr_eeg.crop(0.1, 0.1)
```

### Step 17: Call pytest.raises()

```python
pytest.raises(RuntimeError, tfr_meg.add_channels, [tfr_badsf])
```

### Step 18: Call pytest.raises()

```python
pytest.raises(ValueError, tfr_meg.add_channels, [tfr_eeg])
```

### Step 19: Call pytest.raises()

```python
pytest.raises(ValueError, tfr_meg.add_channels, [tfr_meg])
```

### Step 20: Call pytest.raises()

```python
pytest.raises(TypeError, tfr_meg.add_channels, tfr_badsf)
```

### Step 21: Assign tfr1 = EpochsTFRArray(...)

```python
tfr1 = EpochsTFRArray(info=mne.create_info(['EEG 001'], 1000, 'eeg'), data=np.zeros((5, 1, 2, 3)), times=[0.1, 0.2, 0.3], freqs=[0.1, 0.2])
```

### Step 22: Assign tfr2 = EpochsTFRArray(...)

```python
tfr2 = EpochsTFRArray(info=mne.create_info(['EEG 002', 'EEG 003'], 1000, 'eeg'), data=np.zeros((5, 2, 2, 3)), times=[0.1, 0.2, 0.3], freqs=[0.1, 0.2])
```

### Step 23: Call tfr1.add_channels()

```python
tfr1.add_channels([tfr2])
```

**Verification:**
```python
assert tfr1.ch_names == ['EEG 001', 'EEG 002', 'EEG 003']
```

### Step 24: Assign unknown = 3.1415927

```python
tfr_badsf.info['sfreq'] = 3.1415927
```


## Complete Example

```python
# Workflow
'Test tfr splitting / re-appending channel types.'
data = np.zeros((6, 2, 3))
times = np.array([0.1, 0.2, 0.3])
freqs = np.array([0.1, 0.2])
info = mne.create_info(['MEG 001', 'MEG 002', 'MEG 003', 'EEG 001', 'EEG 002', 'STIM 001'], 1000.0, ['mag', 'mag', 'mag', 'eeg', 'eeg', 'stim'])
tfr = AverageTFRArray(info=info, data=data, times=times, freqs=freqs, nave=20, comment='test', method='crazy-tfr')
tfr_eeg = tfr.copy().pick(picks='eeg')
tfr_meg = tfr.copy().pick(picks='meg')
tfr_stim = tfr.copy().pick(picks='stim')
tfr_eeg_meg = tfr.copy().pick(picks=['meg', 'eeg'])
tfr_new = tfr_meg.copy().add_channels([tfr_eeg, tfr_stim])
assert all((ch in tfr_new.ch_names for ch in tfr_stim.ch_names + tfr_meg.ch_names))
tfr_new = tfr_meg.copy().add_channels([tfr_eeg])
have_all = all((ch in tfr_new.ch_names for ch in tfr.ch_names if ch != 'STIM 001'))
assert have_all
assert_array_equal(tfr_new.data, tfr_eeg_meg.data)
assert all((ch not in tfr_new.ch_names for ch in tfr_stim.ch_names))
tfr_badsf = tfr_eeg.copy()
with tfr_badsf.info._unlock():
    tfr_badsf.info['sfreq'] = 3.1415927
tfr_eeg = tfr_eeg.crop(0.1, 0.1)
pytest.raises(RuntimeError, tfr_meg.add_channels, [tfr_badsf])
pytest.raises(ValueError, tfr_meg.add_channels, [tfr_eeg])
pytest.raises(ValueError, tfr_meg.add_channels, [tfr_meg])
pytest.raises(TypeError, tfr_meg.add_channels, tfr_badsf)
tfr1 = EpochsTFRArray(info=mne.create_info(['EEG 001'], 1000, 'eeg'), data=np.zeros((5, 1, 2, 3)), times=[0.1, 0.2, 0.3], freqs=[0.1, 0.2])
tfr2 = EpochsTFRArray(info=mne.create_info(['EEG 002', 'EEG 003'], 1000, 'eeg'), data=np.zeros((5, 2, 2, 3)), times=[0.1, 0.2, 0.3], freqs=[0.1, 0.2])
tfr1.add_channels([tfr2])
assert tfr1.ch_names == ['EEG 001', 'EEG 002', 'EEG 003']
assert tfr1.data.shape == (5, 3, 2, 3)
```

## Next Steps


---

*Source: test_tfr.py:981 | Complexity: Advanced | Last updated: 2026-05-18*