# How To: Interpolation Ecog

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test interpolation for ECoG.

## Prerequisites

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.channels`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.proj`
- `mne.channels`
- `mne.channels.interpolation`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.utils`
- `mne.channels.interpolation`


## Step-by-Step Guide

### Step 1: 'Test interpolation for ECoG.'

```python
'Test interpolation for ECoG.'
```

**Verification:**
```python
assert not np.all(raw_before._data[bads_mask] == raw_after._data[bads_mask])
```

### Step 2: Assign unknown = _load_data(...)

```python
raw, epochs_eeg = _load_data('eeg')
```

**Verification:**
```python
assert_array_equal(raw_before._data[~bads_mask], raw_after._data[~bads_mask])
```

### Step 3: Assign bads = value

```python
bads = ['EEG 012']
```

### Step 4: Assign bads_mask = np.isin(...)

```python
bads_mask = np.isin(epochs_eeg.ch_names, bads)
```

### Step 5: Assign epochs_ecog = epochs_eeg.set_channel_types(...)

```python
epochs_ecog = epochs_eeg.set_channel_types({ch: 'ecog' for ch in epochs_eeg.ch_names})
```

### Step 6: Assign unknown = bads

```python
epochs_ecog.info['bads'] = bads
```

### Step 7: Assign raw_ecog = RawArray(...)

```python
raw_ecog = RawArray(data=epochs_ecog._data[0], info=epochs_ecog.info)
```

### Step 8: Assign raw_before = raw_ecog.copy(...)

```python
raw_before = raw_ecog.copy()
```

### Step 9: Assign raw_after = raw_ecog.interpolate_bads(...)

```python
raw_after = raw_ecog.interpolate_bads(method=dict(ecog='spline'))
```

**Verification:**
```python
assert not np.all(raw_before._data[bads_mask] == raw_after._data[bads_mask])
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(raw_before._data[~bads_mask], raw_after._data[~bads_mask])
```


## Complete Example

```python
# Workflow
'Test interpolation for ECoG.'
raw, epochs_eeg = _load_data('eeg')
bads = ['EEG 012']
bads_mask = np.isin(epochs_eeg.ch_names, bads)
epochs_ecog = epochs_eeg.set_channel_types({ch: 'ecog' for ch in epochs_eeg.ch_names})
epochs_ecog.info['bads'] = bads
raw_ecog = RawArray(data=epochs_ecog._data[0], info=epochs_ecog.info)
raw_before = raw_ecog.copy()
raw_after = raw_ecog.interpolate_bads(method=dict(ecog='spline'))
assert not np.all(raw_before._data[bads_mask] == raw_after._data[bads_mask])
assert_array_equal(raw_before._data[~bads_mask], raw_after._data[~bads_mask])
```

## Next Steps


---

*Source: test_interpolation.py:375 | Complexity: Advanced | Last updated: 2026-05-18*