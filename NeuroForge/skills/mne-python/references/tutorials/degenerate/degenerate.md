# How To: Degenerate

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test some degenerate conditions.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test some degenerate conditions.'

```python
'Test some degenerate conditions.'
```

### Step 2: Assign eeg = value

```python
eeg = io.loadmat(epochs_fname_mat, struct_as_record=False, squeeze_me=True)['EEG']
```

### Step 3: Assign eeg.data = 'epochs_fname.dat'

```python
eeg.data = 'epochs_fname.dat'
```

### Step 4: Assign bad_epochs_fname = value

```python
bad_epochs_fname = tmp_path / 'test_epochs.set'
```

### Step 5: Call io.savemat()

```python
io.savemat(bad_epochs_fname, {'EEG': {'trials': eeg.trials, 'srate': eeg.srate, 'nbchan': eeg.nbchan, 'data': eeg.data, 'epoch': eeg.epoch, 'event': eeg.event, 'chanlocs': eeg.chanlocs, 'pnts': eeg.pnts}}, appendmat=False, oned_as='row')
```

### Step 6: Call shutil.copyfile()

```python
shutil.copyfile(base_dir / 'test_epochs.fdt', tmp_path / 'test_epochs.dat')
```

### Step 7: Call pytest.raises()

```python
pytest.raises(NotImplementedError, read_epochs_eeglab, bad_epochs_fname)
```

### Step 8: Assign m_fname = value

```python
m_fname = tmp_path / 'test_montage_m.set'
```

### Step 9: Call _create_eeg_with_scaled_montage_units()

```python
_create_eeg_with_scaled_montage_units(raw_fname_chanloc, m_fname, 0.001)
```

### Step 10: Call read_epochs_eeglab()

```python
read_epochs_eeglab(epochs_fname_mat, montage_units='mV')
```

### Step 11: Call read_raw_eeglab()

```python
read_raw_eeglab(raw_fname_chanloc, montage_units='m')
```

### Step 12: Call read_raw_eeglab()

```python
read_raw_eeglab(m_fname, montage_units='mm')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test some degenerate conditions.'
eeg = io.loadmat(epochs_fname_mat, struct_as_record=False, squeeze_me=True)['EEG']
eeg.data = 'epochs_fname.dat'
bad_epochs_fname = tmp_path / 'test_epochs.set'
io.savemat(bad_epochs_fname, {'EEG': {'trials': eeg.trials, 'srate': eeg.srate, 'nbchan': eeg.nbchan, 'data': eeg.data, 'epoch': eeg.epoch, 'event': eeg.event, 'chanlocs': eeg.chanlocs, 'pnts': eeg.pnts}}, appendmat=False, oned_as='row')
shutil.copyfile(base_dir / 'test_epochs.fdt', tmp_path / 'test_epochs.dat')
pytest.raises(NotImplementedError, read_epochs_eeglab, bad_epochs_fname)
with pytest.raises(ValueError, match='Invalid value'):
    read_epochs_eeglab(epochs_fname_mat, montage_units='mV')
with pytest.warns(RuntimeWarning, match='is above'):
    read_raw_eeglab(raw_fname_chanloc, montage_units='m')
m_fname = tmp_path / 'test_montage_m.set'
_create_eeg_with_scaled_montage_units(raw_fname_chanloc, m_fname, 0.001)
with pytest.warns(RuntimeWarning, match='is below'):
    read_raw_eeglab(m_fname, montage_units='mm')
```

## Next Steps


---

*Source: test_eeglab.py:400 | Complexity: Advanced | Last updated: 2026-05-18*