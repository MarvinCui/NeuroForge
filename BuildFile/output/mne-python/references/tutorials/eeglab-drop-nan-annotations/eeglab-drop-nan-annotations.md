# How To: Eeglab Drop Nan Annotations

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading file with NaN annotations.

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

### Step 1: 'Test reading file with NaN annotations.'

```python
'Test reading file with NaN annotations.'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('eeglabio')
```

### Step 3: Assign file_path = value

```python
file_path = tmp_path / 'test_nan_anno.set'
```

### Step 4: Assign raw = read_raw_eeglab(...)

```python
raw = read_raw_eeglab(raw_fname_mat, preload=True)
```

### Step 5: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

### Step 6: Assign sfreq = value

```python
sfreq = raw.info['sfreq']
```

### Step 7: Assign ch_names = value

```python
ch_names = raw.ch_names
```

### Step 8: Assign anno = value

```python
anno = [raw.annotations.description, raw.annotations.onset, raw.annotations.duration]
```

### Step 9: Assign unknown = value

```python
anno[1][0] = np.nan
```

### Step 10: Call export_set()

```python
export_set(str(file_path), data, sfreq, ch_names, ch_locs=None, annotations=anno, ref_channels='common', ch_types=np.repeat('EEG', len(ch_names)))
```

### Step 11: Assign raw = read_raw_eeglab(...)

```python
raw = read_raw_eeglab(file_path, preload=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading file with NaN annotations.'
pytest.importorskip('eeglabio')
from eeglabio.raw import export_set
file_path = tmp_path / 'test_nan_anno.set'
raw = read_raw_eeglab(raw_fname_mat, preload=True)
data = raw.get_data()
sfreq = raw.info['sfreq']
ch_names = raw.ch_names
anno = [raw.annotations.description, raw.annotations.onset, raw.annotations.duration]
anno[1][0] = np.nan
export_set(str(file_path), data, sfreq, ch_names, ch_locs=None, annotations=anno, ref_channels='common', ch_types=np.repeat('EEG', len(ch_names)))
with pytest.warns(RuntimeWarning, match='1 .* have an onset that is NaN.*'):
    raw = read_raw_eeglab(file_path, preload=True)
```

## Next Steps


---

*Source: test_eeglab.py:739 | Complexity: Advanced | Last updated: 2026-05-18*