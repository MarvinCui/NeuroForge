# How To: Csd Epochs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test making epochs, saving to disk and loading.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test making epochs, saving to disk and loading.'

```python
'Test making epochs, saving to disk and loading.'
```

**Verification:**
```python
assert_allclose(epochs._data, epochs2._data)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

### Step 3: Call raw.pick.load_data()

```python
raw.pick(picks=['eeg', 'stim']).load_data()
```

### Step 4: Assign events = find_events(...)

```python
events = find_events(raw)
```

### Step 5: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, reject=dict(eeg=0.0001), preload=True)
```

### Step 6: Assign epochs = compute_current_source_density(...)

```python
epochs = compute_current_source_density(epochs)
```

### Step 7: Assign epo_fname = value

```python
epo_fname = tmp_path / 'test_csd_epo.fif'
```

### Step 8: Call epochs.save()

```python
epochs.save(epo_fname)
```

### Step 9: Assign epochs2 = read_epochs(...)

```python
epochs2 = read_epochs(epo_fname, preload=True)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(epochs._data, epochs2._data)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test making epochs, saving to disk and loading.'
raw = read_raw_fif(raw_fname)
raw.pick(picks=['eeg', 'stim']).load_data()
events = find_events(raw)
epochs = Epochs(raw, events, reject=dict(eeg=0.0001), preload=True)
epochs = compute_current_source_density(epochs)
epo_fname = tmp_path / 'test_csd_epo.fif'
epochs.save(epo_fname)
epochs2 = read_epochs(epo_fname, preload=True)
assert_allclose(epochs._data, epochs2._data)
```

## Next Steps


---

*Source: test_csd.py:190 | Complexity: Advanced | Last updated: 2026-05-18*