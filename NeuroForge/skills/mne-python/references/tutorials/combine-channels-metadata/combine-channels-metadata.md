# How To: Combine Channels Metadata

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if metadata is correctly retained in combined object.

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

### Step 1: 'Test if metadata is correctly retained in combined object.'

```python
'Test if metadata is correctly retained in combined object.'
```

### Step 2: Assign pd = pytest.importorskip(...)

```python
pd = pytest.importorskip('pandas')
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=True)
```

### Step 4: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, read_events(eve_fname), preload=True)
```

### Step 5: Assign metadata = pd.DataFrame(...)

```python
metadata = pd.DataFrame({'A': np.arange(len(epochs)), 'B': np.ones(len(epochs))})
```

### Step 6: Assign epochs.metadata = metadata

```python
epochs.metadata = metadata
```

### Step 7: Assign good = dict(...)

```python
good = dict(foo=[0, 1, 3, 4], bar=[5, 2])
```

### Step 8: Assign combined_epochs = combine_channels(...)

```python
combined_epochs = combine_channels(epochs, good)
```

### Step 9: Call pd.testing.assert_frame_equal()

```python
pd.testing.assert_frame_equal(epochs.metadata, combined_epochs.metadata)
```


## Complete Example

```python
# Workflow
'Test if metadata is correctly retained in combined object.'
pd = pytest.importorskip('pandas')
raw = read_raw_fif(raw_fname, preload=True)
epochs = Epochs(raw, read_events(eve_fname), preload=True)
metadata = pd.DataFrame({'A': np.arange(len(epochs)), 'B': np.ones(len(epochs))})
epochs.metadata = metadata
good = dict(foo=[0, 1, 3, 4], bar=[5, 2])
combined_epochs = combine_channels(epochs, good)
pd.testing.assert_frame_equal(epochs.metadata, combined_epochs.metadata)
```

## Next Steps


---

*Source: test_channels.py:687 | Complexity: Advanced | Last updated: 2026-05-18*