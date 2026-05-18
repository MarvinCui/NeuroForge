# How To: Events From Annotation Orig Time None

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Tests events_from_annotation with orig_time None and first_sampe > 0.

## Prerequisites

**Required Modules:**
- `sys`
- `collections`
- `datetime`
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `pytest`
- `mne`
- `mne`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Tests events_from_annotation with orig_time None and first_sampe > 0.'

```python
'Tests events_from_annotation with orig_time None and first_sampe > 0.'
```

**Verification:**
```python
assert_array_equal(epochs.get_data()[0], data[:, 800:901])
```

### Step 2: Assign unknown = value

```python
sfreq, duration_s = (100, 10)
```

### Step 3: Assign data = np.random.RandomState.randn(...)

```python
data = np.random.RandomState(42).randn(1, sfreq * duration_s)
```

### Step 4: Assign info = mne.create_info(...)

```python
info = mne.create_info(ch_names=['EEG1'], ch_types=['eeg'], sfreq=sfreq)
```

### Step 5: Assign raw = mne.io.RawArray(...)

```python
raw = mne.io.RawArray(data, info)
```

### Step 6: Assign onset = value

```python
onset = [8]
```

### Step 7: Assign duration = value

```python
duration = [1]
```

### Step 8: Assign description = value

```python
description = ['0']
```

### Step 9: Assign annots = mne.Annotations(...)

```python
annots = mne.Annotations(onset, duration, description)
```

### Step 10: Assign raw = raw.set_annotations(...)

```python
raw = raw.set_annotations(annots)
```

### Step 11: Call raw.crop()

```python
raw.crop(tmin=7)
```

### Step 12: Assign unknown = mne.events_from_annotations(...)

```python
events, event_ids = mne.events_from_annotations(raw)
```

### Step 13: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, tmin=0, tmax=1, baseline=None, on_missing='warning')
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(epochs.get_data()[0], data[:, 800:901])
```


## Complete Example

```python
# Workflow
'Tests events_from_annotation with orig_time None and first_sampe > 0.'
sfreq, duration_s = (100, 10)
data = np.random.RandomState(42).randn(1, sfreq * duration_s)
info = mne.create_info(ch_names=['EEG1'], ch_types=['eeg'], sfreq=sfreq)
raw = mne.io.RawArray(data, info)
onset = [8]
duration = [1]
description = ['0']
annots = mne.Annotations(onset, duration, description)
raw = raw.set_annotations(annots)
raw.crop(tmin=7)
events, event_ids = mne.events_from_annotations(raw)
epochs = mne.Epochs(raw, events, tmin=0, tmax=1, baseline=None, on_missing='warning')
assert_array_equal(epochs.get_data()[0], data[:, 800:901])
```

## Next Steps


---

*Source: test_annotations.py:338 | Complexity: Advanced | Last updated: 2026-05-18*