# How To: Eeglab Event From Annot

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test all forms of obtaining annotations.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test all forms of obtaining annotations.'

```python
'Test all forms of obtaining annotations.'
```

**Verification:**
```python
assert len(raw1.annotations) == 154
```

### Step 2: Assign raw_fname_mat = value

```python
raw_fname_mat = base_dir / 'test_raw.set'
```

**Verification:**
```python
assert len(events_b) == 154
```

### Step 3: Assign raw_fname = raw_fname_mat

```python
raw_fname = raw_fname_mat
```

### Step 4: Assign event_id = value

```python
event_id = {'rt': 1, 'square': 2}
```

### Step 5: Assign raw1 = read_raw_eeglab(...)

```python
raw1 = read_raw_eeglab(input_fname=raw_fname, preload=False)
```

### Step 6: Assign annotations = read_annotations(...)

```python
annotations = read_annotations(raw_fname)
```

**Verification:**
```python
assert len(raw1.annotations) == 154
```

### Step 7: Call raw1.set_annotations()

```python
raw1.set_annotations(annotations)
```

### Step 8: Assign unknown = events_from_annotations(...)

```python
events_b, _ = events_from_annotations(raw1, event_id=event_id)
```

**Verification:**
```python
assert len(events_b) == 154
```


## Complete Example

```python
# Workflow
'Test all forms of obtaining annotations.'
raw_fname_mat = base_dir / 'test_raw.set'
raw_fname = raw_fname_mat
event_id = {'rt': 1, 'square': 2}
raw1 = read_raw_eeglab(input_fname=raw_fname, preload=False)
annotations = read_annotations(raw_fname)
assert len(raw1.annotations) == 154
raw1.set_annotations(annotations)
events_b, _ = events_from_annotations(raw1, event_id=event_id)
assert len(events_b) == 154
```

## Next Steps


---

*Source: test_eeglab.py:494 | Complexity: Advanced | Last updated: 2026-05-18*