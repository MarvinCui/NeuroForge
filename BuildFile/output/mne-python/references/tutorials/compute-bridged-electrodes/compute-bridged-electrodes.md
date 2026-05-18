# How To: Compute Bridged Electrodes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test computing bridged electrodes.

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

### Step 1: 'Test computing bridged electrodes.'

```python
'Test computing bridged electrodes.'
```

**Verification:**
```python
assert bridged_idx == [(idx0, idx1)]
```

### Step 2: Assign raw = read_raw_fif.load_data(...)

```python
raw = read_raw_fif(raw_fname).load_data()
```

**Verification:**
```python
assert ed_matrix.shape == (raw.times.size // (epoch_duration * raw.info['sfreq']), picks.size, picks.size)
```

### Step 3: Call raw.pick()

```python
raw.pick(picks='meg')
```

**Verification:**
```python
assert np.all(ed_matrix[:, picks.index(idx0), picks.index(idx1)] == 0)
```

### Step 4: Assign epoch_duration = 3

```python
epoch_duration = 3
```

**Verification:**
```python
assert np.all(np.isnan(ed_matrix[0][np.tril_indices(len(picks), -1)]))
```

### Step 5: Assign raw = read_raw_fif.load_data(...)

```python
raw = read_raw_fif(raw_fname).load_data()
```

### Step 6: Assign idx0 = raw.ch_names.index(...)

```python
idx0 = raw.ch_names.index('EEG 001')
```

### Step 7: Assign idx1 = raw.ch_names.index(...)

```python
idx1 = raw.ch_names.index('EEG 002')
```

### Step 8: Assign unknown = value

```python
raw._data[idx1] = raw._data[idx0]
```

### Step 9: Assign unknown = compute_bridged_electrodes(...)

```python
bridged_idx, ed_matrix = compute_bridged_electrodes(raw, epoch_duration=epoch_duration)
```

**Verification:**
```python
assert bridged_idx == [(idx0, idx1)]
```

### Step 10: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=False, eeg=True)
```

**Verification:**
```python
assert ed_matrix.shape == (raw.times.size // (epoch_duration * raw.info['sfreq']), picks.size, picks.size)
```

### Step 11: Assign picks = list(...)

```python
picks = list(picks)
```

**Verification:**
```python
assert np.all(ed_matrix[:, picks.index(idx0), picks.index(idx1)] == 0)
```

### Step 12: Assign unknown = compute_bridged_electrodes(...)

```python
bridged_idx, ed_matrix = compute_bridged_electrodes(raw)
```


## Complete Example

```python
# Workflow
'Test computing bridged electrodes.'
raw = read_raw_fif(raw_fname).load_data()
raw.pick(picks='meg')
with pytest.raises(RuntimeError, match='No EEG channels found'):
    bridged_idx, ed_matrix = compute_bridged_electrodes(raw)
epoch_duration = 3
raw = read_raw_fif(raw_fname).load_data()
idx0 = raw.ch_names.index('EEG 001')
idx1 = raw.ch_names.index('EEG 002')
raw._data[idx1] = raw._data[idx0]
bridged_idx, ed_matrix = compute_bridged_electrodes(raw, epoch_duration=epoch_duration)
assert bridged_idx == [(idx0, idx1)]
picks = pick_types(raw.info, meg=False, eeg=True)
assert ed_matrix.shape == (raw.times.size // (epoch_duration * raw.info['sfreq']), picks.size, picks.size)
picks = list(picks)
assert np.all(ed_matrix[:, picks.index(idx0), picks.index(idx1)] == 0)
assert np.all(np.isnan(ed_matrix[0][np.tril_indices(len(picks), -1)]))
```

## Next Steps


---

*Source: test_csd.py:203 | Complexity: Advanced | Last updated: 2026-05-18*