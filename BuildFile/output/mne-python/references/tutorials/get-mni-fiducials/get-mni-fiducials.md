# How To: Get Mni Fiducials

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test get_mni_fiducials.

## Prerequisites

**Required Modules:**
- `os`
- `functools`
- `glob`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.source_space`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test get_mni_fiducials.'

```python
'Test get_mni_fiducials.'
```

**Verification:**
```python
assert coord_frame == FIFF.FIFFV_COORD_MRI
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert [f['ident'] for f in fids] == list(range(1, 4))
```

### Step 3: Assign unknown = read_fiducials(...)

```python
fids, coord_frame = read_fiducials(fid_fname)
```

**Verification:**
```python
assert (dists < 8).all(), dists
```

### Step 4: Assign fids = np.array(...)

```python
fids = np.array([f['r'] for f in fids])
```

### Step 5: Assign fids_est = get_mni_fiducials(...)

```python
fids_est = get_mni_fiducials('sample', subjects_dir)
```

### Step 6: Assign fids_est = np.array(...)

```python
fids_est = np.array([f['r'] for f in fids_est])
```

### Step 7: Assign dists = value

```python
dists = np.linalg.norm(fids - fids_est, axis=-1) * 1000.0
```

**Verification:**
```python
assert (dists < 8).all(), dists
```


## Complete Example

```python
# Workflow
'Test get_mni_fiducials.'
pytest.importorskip('nibabel')
fids, coord_frame = read_fiducials(fid_fname)
assert coord_frame == FIFF.FIFFV_COORD_MRI
assert [f['ident'] for f in fids] == list(range(1, 4))
fids = np.array([f['r'] for f in fids])
fids_est = get_mni_fiducials('sample', subjects_dir)
fids_est = np.array([f['r'] for f in fids_est])
dists = np.linalg.norm(fids - fids_est, axis=-1) * 1000.0
assert (dists < 8).all(), dists
```

## Next Steps


---

*Source: test_coreg.py:384 | Complexity: Intermediate | Last updated: 2026-05-18*