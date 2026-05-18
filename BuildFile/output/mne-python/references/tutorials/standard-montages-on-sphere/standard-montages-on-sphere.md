# How To: Standard Montages On Sphere

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test some standard montage are on sphere.

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
# Fixtures: kind, tol, head_size
```

## Step-by-Step Guide

### Step 1: 'Test some standard montage are on sphere.'

```python
'Test some standard montage are on sphere.'
```

**Verification:**
```python
assert_allclose(actual=np.linalg.norm(eeg_loc, axis=1), desired=np.full((eeg_loc.shape[0],), head_size), atol=tol)
```

### Step 2: Assign kwargs = dict(...)

```python
kwargs = dict()
```

### Step 3: Assign montage = make_standard_montage(...)

```python
montage = make_standard_montage(kind, **kwargs)
```

### Step 4: Assign eeg_loc = np.array(...)

```python
eeg_loc = np.array([ch['r'] for ch in _get_dig_eeg(montage.dig)])
```

### Step 5: Call assert_allclose()

```python
assert_allclose(actual=np.linalg.norm(eeg_loc, axis=1), desired=np.full((eeg_loc.shape[0],), head_size), atol=tol)
```

### Step 6: Assign unknown = head_size

```python
kwargs['head_size'] = head_size
```


## Complete Example

```python
# Setup
# Fixtures: kind, tol, head_size

# Workflow
'Test some standard montage are on sphere.'
kwargs = dict()
if head_size != HEAD_SIZE_DEFAULT:
    kwargs['head_size'] = head_size
montage = make_standard_montage(kind, **kwargs)
eeg_loc = np.array([ch['r'] for ch in _get_dig_eeg(montage.dig)])
assert_allclose(actual=np.linalg.norm(eeg_loc, axis=1), desired=np.full((eeg_loc.shape[0],), head_size), atol=tol)
```

## Next Steps


---

*Source: test_standard_montage.py:58 | Complexity: Intermediate | Last updated: 2026-05-18*