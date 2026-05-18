# How To: Io Set Epochs Events

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test different combinations of events and event_ids.

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

### Step 1: 'Test different combinations of events and event_ids.'

```python
'Test different combinations of events and event_ids.'
```

**Verification:**
```python
assert_equal(len(epochs.events), 4)
```

### Step 2: Assign out_fname = value

```python
out_fname = tmp_path / 'test-eve.fif'
```

**Verification:**
```python
assert epochs.preload
```

### Step 3: Assign events = np.array(...)

```python
events = np.array([[4, 0, 1], [12, 0, 2], [20, 0, 3], [26, 0, 3]])
```

**Verification:**
```python
assert epochs._bad_dropped
```

### Step 4: Call write_events()

```python
write_events(out_fname, events)
```

### Step 5: Assign event_id = value

```python
event_id = {'S255/S8': 1, 'S8': 2, 'S255/S9': 3}
```

### Step 6: Assign epochs = read_epochs_eeglab(...)

```python
epochs = read_epochs_eeglab(epochs_fname_mat, events, event_id)
```

### Step 7: Call assert_equal()

```python
assert_equal(len(epochs.events), 4)
```

**Verification:**
```python
assert epochs.preload
```

### Step 8: Assign epochs = read_epochs_eeglab(...)

```python
epochs = read_epochs_eeglab(epochs_fname_mat, out_fname, event_id)
```

### Step 9: Call pytest.raises()

```python
pytest.raises(ValueError, read_epochs_eeglab, epochs_fname_mat, None, event_id)
```

### Step 10: Call pytest.raises()

```python
pytest.raises(ValueError, read_epochs_eeglab, epochs_fname_mat, epochs.events, None)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test different combinations of events and event_ids.'
out_fname = tmp_path / 'test-eve.fif'
events = np.array([[4, 0, 1], [12, 0, 2], [20, 0, 3], [26, 0, 3]])
write_events(out_fname, events)
event_id = {'S255/S8': 1, 'S8': 2, 'S255/S9': 3}
epochs = read_epochs_eeglab(epochs_fname_mat, events, event_id)
assert_equal(len(epochs.events), 4)
assert epochs.preload
assert epochs._bad_dropped
epochs = read_epochs_eeglab(epochs_fname_mat, out_fname, event_id)
pytest.raises(ValueError, read_epochs_eeglab, epochs_fname_mat, None, event_id)
pytest.raises(ValueError, read_epochs_eeglab, epochs_fname_mat, epochs.events, None)
```

## Next Steps


---

*Source: test_eeglab.py:382 | Complexity: Advanced | Last updated: 2026-05-18*