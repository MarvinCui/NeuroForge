# How To: Fil Complete

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test FIL reader, match to known answers from .mat file.

## Prerequisites

**Required Modules:**
- `os`
- `pytest`
- `scipy.io`
- `numpy`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.io.fil.sensors`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test FIL reader, match to known answers from .mat file.'

```python
'Test FIL reader, match to known answers from .mat file.'
```

### Step 2: Assign binname = value

```python
binname = fil_path / 'sub-noise_ses-001_task-noise220622_run-001_meg.bin'
```

### Step 3: Assign matname = value

```python
matname = fil_path / 'sub-noise_ses-001_task-noise220622_run-001_fieldtrip.mat'
```

### Step 4: Assign raw = read_raw_fil(...)

```python
raw = read_raw_fil(binname)
```

### Step 5: Call raw.load_data()

```python
raw.load_data(verbose=False)
```

### Step 6: Assign tmp = scipy.io.loadmat(...)

```python
tmp = scipy.io.loadmat(matname)
```

### Step 7: Assign mat = unpack_mat(...)

```python
mat = unpack_mat(tmp)
```

### Step 8: Call _fil_megmag()

```python
_fil_megmag(raw, mat)
```

### Step 9: Call _fil_stim()

```python
_fil_stim(raw, mat)
```

### Step 10: Call _fil_sensorpos()

```python
_fil_sensorpos(raw, mat)
```


## Complete Example

```python
# Workflow
'Test FIL reader, match to known answers from .mat file.'
binname = fil_path / 'sub-noise_ses-001_task-noise220622_run-001_meg.bin'
matname = fil_path / 'sub-noise_ses-001_task-noise220622_run-001_fieldtrip.mat'
raw = read_raw_fil(binname)
raw.load_data(verbose=False)
tmp = scipy.io.loadmat(matname)
mat = unpack_mat(tmp)
_fil_megmag(raw, mat)
_fil_stim(raw, mat)
_fil_sensorpos(raw, mat)
```

## Next Steps


---

*Source: test_fil.py:145 | Complexity: Advanced | Last updated: 2026-05-18*