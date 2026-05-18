# How To: Epochs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading epoched SQD file.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.kit.constants`
- `mne.io.kit.coreg`
- `mne.io.kit.kit`
- `mne.io.tests.test_raw`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test reading epoched SQD file.'

```python
'Test reading epoched SQD file.'
```

**Verification:**
```python
assert_array_equal(data1, data11)
```

### Step 2: Assign raw = read_raw_kit(...)

```python
raw = read_raw_kit(sqd_path, stim=None)
```

### Step 3: Assign events = read_events(...)

```python
events = read_events(events_path)
```

### Step 4: Assign raw_epochs = Epochs(...)

```python
raw_epochs = Epochs(raw, events, None, tmin=0, tmax=0.099, baseline=None)
```

### Step 5: Assign data1 = raw_epochs.get_data(...)

```python
data1 = raw_epochs.get_data(copy=False)
```

### Step 6: Assign epochs = read_epochs_kit(...)

```python
epochs = read_epochs_kit(epochs_path, events_path)
```

### Step 7: Assign data11 = epochs.get_data(...)

```python
data11 = epochs.get_data(copy=False)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(data1, data11)
```


## Complete Example

```python
# Workflow
'Test reading epoched SQD file.'
raw = read_raw_kit(sqd_path, stim=None)
events = read_events(events_path)
raw_epochs = Epochs(raw, events, None, tmin=0, tmax=0.099, baseline=None)
data1 = raw_epochs.get_data(copy=False)
epochs = read_epochs_kit(epochs_path, events_path)
data11 = epochs.get_data(copy=False)
assert_array_equal(data1, data11)
```

## Next Steps


---

*Source: test_kit.py:284 | Complexity: Advanced | Last updated: 2026-05-18*