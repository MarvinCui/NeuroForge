# How To: Add Reference Channels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if there is a new reference channel that consist of all zeros.

## Prerequisites

**Required Modules:**
- `hashlib`
- `contextlib`
- `copy`
- `functools`
- `pathlib`
- `numpy`
- `pooch`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.channels.channels`
- `mne.datasets`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test if there is a new reference channel that consist of all zeros.'

```python
'Test if there is a new reference channel that consist of all zeros.'
```

**Verification:**
```python
assert len(raw.ch_names) == n_raw_original_channels + 1
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=True)
```

**Verification:**
```python
assert np.all(raw.get_data()[-1] == 0)
```

### Step 3: Assign n_raw_original_channels = len(...)

```python
n_raw_original_channels = len(raw.ch_names)
```

**Verification:**
```python
assert epochs._data.shape[1] == epochs_original_shape + 1
```

### Step 4: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, read_events(eve_fname))
```

**Verification:**
```python
assert len(evoked.ch_names) == n_evoked_original_channels + 1
```

### Step 5: Call epochs.load_data()

```python
epochs.load_data()
```

**Verification:**
```python
assert np.all(evoked._data[-1] == 0)
```

### Step 6: Assign epochs_original_shape = value

```python
epochs_original_shape = epochs._data.shape[1]
```

### Step 7: Assign evoked = epochs.average(...)

```python
evoked = epochs.average()
```

### Step 8: Assign n_evoked_original_channels = len(...)

```python
n_evoked_original_channels = len(evoked.ch_names)
```

### Step 9: Call raw.add_reference_channels()

```python
raw.add_reference_channels(['REF 123'])
```

**Verification:**
```python
assert len(raw.ch_names) == n_raw_original_channels + 1
```

### Step 10: Call epochs.add_reference_channels()

```python
epochs.add_reference_channels(['REF 123'])
```

**Verification:**
```python
assert epochs._data.shape[1] == epochs_original_shape + 1
```

### Step 11: Call evoked.add_reference_channels()

```python
evoked.add_reference_channels(['REF 123'])
```

**Verification:**
```python
assert len(evoked.ch_names) == n_evoked_original_channels + 1
```


## Complete Example

```python
# Workflow
'Test if there is a new reference channel that consist of all zeros.'
raw = read_raw_fif(raw_fname, preload=True)
n_raw_original_channels = len(raw.ch_names)
epochs = Epochs(raw, read_events(eve_fname))
epochs.load_data()
epochs_original_shape = epochs._data.shape[1]
evoked = epochs.average()
n_evoked_original_channels = len(evoked.ch_names)
raw.add_reference_channels(['REF 123'])
assert len(raw.ch_names) == n_raw_original_channels + 1
assert np.all(raw.get_data()[-1] == 0)
epochs.add_reference_channels(['REF 123'])
assert epochs._data.shape[1] == epochs_original_shape + 1
evoked.add_reference_channels(['REF 123'])
assert len(evoked.ch_names) == n_evoked_original_channels + 1
assert np.all(evoked._data[-1] == 0)
```

## Next Steps


---

*Source: test_channels.py:537 | Complexity: Advanced | Last updated: 2026-05-18*