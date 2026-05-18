# How To: Has Source Detector Distances

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Ensure source-detector distance availability is detected.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.datasets.testing`
- `mne.io`
- `mne.preprocessing.nirs`


## Step-by-Step Guide

### Step 1: 'Ensure source-detector distance availability is detected.'

```python
'Ensure source-detector distance availability is detected.'
```

**Verification:**
```python
assert not _has_source_detector_distances(info)
```

### Step 2: Assign ch_names = value

```python
ch_names = ['S1_D1 760', 'S1_D1 850', 'S2_D1 760', 'S2_D1 850']
```

**Verification:**
```python
assert _has_source_detector_distances(info, picks=[0, 1])
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, ch_types=np.repeat('fnirs_od', 4), sfreq=1.0)
```

**Verification:**
```python
assert not _has_source_detector_distances(info)
```

### Step 4: Assign unknown = value

```python
info['chs'][idx]['loc'][3:6] = [0.0, 0.0, 0.0]
```

**Verification:**
```python
assert _has_source_detector_distances(info)
```

### Step 5: Assign unknown = value

```python
info['chs'][idx]['loc'][6:9] = [0.03, 0.0, 0.0]
```

### Step 6: Assign unknown = value

```python
info['chs'][idx]['loc'][3:6] = [0.01, 0.0, 0.0]
```

### Step 7: Assign unknown = value

```python
info['chs'][idx]['loc'][6:9] = [0.04, 0.0, 0.0]
```


## Complete Example

```python
# Workflow
'Ensure source-detector distance availability is detected.'
ch_names = ['S1_D1 760', 'S1_D1 850', 'S2_D1 760', 'S2_D1 850']
info = create_info(ch_names=ch_names, ch_types=np.repeat('fnirs_od', 4), sfreq=1.0)
assert not _has_source_detector_distances(info)
for idx in range(2):
    info['chs'][idx]['loc'][3:6] = [0.0, 0.0, 0.0]
    info['chs'][idx]['loc'][6:9] = [0.03, 0.0, 0.0]
assert _has_source_detector_distances(info, picks=[0, 1])
assert not _has_source_detector_distances(info)
for idx in range(2, 4):
    info['chs'][idx]['loc'][3:6] = [0.01, 0.0, 0.0]
    info['chs'][idx]['loc'][6:9] = [0.04, 0.0, 0.0]
assert _has_source_detector_distances(info)
```

## Next Steps


---

*Source: test_nirs.py:542 | Complexity: Intermediate | Last updated: 2026-05-18*