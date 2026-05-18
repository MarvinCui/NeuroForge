# How To: Optical Density Zeromean

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that optical density can process zero mean data.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.datasets`
- `mne.datasets.testing`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test that optical density can process zero mean data.'

```python
'Test that optical density can process zero mean data.'
```

**Verification:**
```python
assert 'fnirs_od' in raw
```

### Step 2: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(fname_nirx, preload=True)
```

### Step 3: Assign unknown = 0

```python
raw._data[4, -1] = 0
```

**Verification:**
```python
assert 'fnirs_od' in raw
```

### Step 4: Assign raw = optical_density(...)

```python
raw = optical_density(raw)
```


## Complete Example

```python
# Workflow
'Test that optical density can process zero mean data.'
raw = read_raw_nirx(fname_nirx, preload=True)
raw._data[4] -= np.mean(raw._data[4])
raw._data[4, -1] = 0
with np.errstate(invalid='raise', divide='raise'):
    with pytest.warns(RuntimeWarning, match='Negative'):
        raw = optical_density(raw)
assert 'fnirs_od' in raw
```

## Next Steps


---

*Source: test_optical_density.py:52 | Complexity: Intermediate | Last updated: 2026-05-18*