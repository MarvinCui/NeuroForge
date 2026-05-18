# How To: Standard Montages Have Fids

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test standard montage are all in unknown coord (have fids).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.channels`
- `mne.channels.montage`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.transforms`

**Setup Required:**
```python
# Fixtures: kind
```

## Step-by-Step Guide

### Step 1: 'Test standard montage are all in unknown coord (have fids).'

```python
'Test standard montage are all in unknown coord (have fids).'
```

**Verification:**
```python
assert v is not None, k
```

### Step 2: Assign montage = make_standard_montage(...)

```python
montage = make_standard_montage(kind)
```

**Verification:**
```python
assert d['coord_frame'] == want
```

### Step 3: Assign unknown = _get_fid_coords(...)

```python
fids, coord_frame = _get_fid_coords(montage.dig)
```

**Verification:**
```python
assert v is not None, k
```

### Step 4: Assign want = value

```python
want = FIFF.FIFFV_COORD_MRI
```

### Step 5: Assign want = value

```python
want = FIFF.FIFFV_COORD_UNKNOWN
```


## Complete Example

```python
# Setup
# Fixtures: kind

# Workflow
'Test standard montage are all in unknown coord (have fids).'
montage = make_standard_montage(kind)
fids, coord_frame = _get_fid_coords(montage.dig)
for k, v in fids.items():
    assert v is not None, k
for d in montage.dig:
    if kind.startswith(('artinis', 'standard', 'mgh')):
        want = FIFF.FIFFV_COORD_MRI
    else:
        want = FIFF.FIFFV_COORD_UNKNOWN
    assert d['coord_frame'] == want
```

## Next Steps


---

*Source: test_standard_montage.py:21 | Complexity: Intermediate | Last updated: 2026-05-18*