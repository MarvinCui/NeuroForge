# How To: Fiducials

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test handling of fiducials.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `shutil`
- `contextlib`
- `functools`
- `itertools`
- `pathlib`
- `string`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.montage`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.channels.montage`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.io.kit`
- `mne.preprocessing`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz._3d`

**Setup Required:**
```python
# Fixtures: tmp_path, fname
```

## Step-by-Step Guide

### Step 1: 'Test handling of fiducials.'

```python
'Test handling of fiducials.'
```

**Verification:**
```python
assert coord_frame == FIFF.FIFFV_COORD_HEAD
```

### Step 2: Assign unknown = read_fiducials(...)

```python
fids, coord_frame = read_fiducials(fname)
```

**Verification:**
```python
assert points.shape == (3, 3)
```

### Step 3: Assign points = _fiducial_coords(...)

```python
points = _fiducial_coords(fids, coord_frame)
```

**Verification:**
```python
assert_allclose(points[:, 2], 0.0, atol=1e-06)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(points[:, 2], 0.0, atol=1e-06)
```

**Verification:**
```python
assert_allclose(points[::2, 1], 0.0, atol=1e-06)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(points[::2, 1], 0.0, atol=1e-06)
```

**Verification:**
```python
assert points[2, 0] > 0
```

### Step 6: Call assert_allclose()

```python
assert_allclose(points[1, 0], 0.0, atol=1e-06)
```

**Verification:**
```python
assert points[0, 0] < 0
```

### Step 7: Assign fname_out = value

```python
fname_out = tmp_path / 'test-dig.fif'
```

**Verification:**
```python
assert_allclose(points[1, 0], 0.0, atol=1e-06)
```

### Step 8: Call make_dig_montage.save()

```python
make_dig_montage(lpa=fids[0]['r'], nasion=fids[1]['r'], rpa=fids[2]['r'], coord_frame='mri_voxel').save(fname_out, overwrite=True)
```

**Verification:**
```python
assert points[1, 1] > 0
```

### Step 9: Assign unknown = read_fiducials(...)

```python
fids_2, coord_frame_2 = read_fiducials(fname_out)
```

**Verification:**
```python
assert coord_frame_2 == FIFF.FIFFV_MNE_COORD_MRI_VOXEL
```

### Step 10: Call assert_allclose()

```python
assert_allclose([fid['r'] for fid in fids[:3]], [fid['r'] for fid in fids_2], rtol=1e-06)
```

**Verification:**
```python
assert_allclose([fid['r'] for fid in fids[:3]], [fid['r'] for fid in fids_2], rtol=1e-06)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fname

# Workflow
'Test handling of fiducials.'
fids, coord_frame = read_fiducials(fname)
assert coord_frame == FIFF.FIFFV_COORD_HEAD
points = _fiducial_coords(fids, coord_frame)
assert points.shape == (3, 3)
assert_allclose(points[:, 2], 0.0, atol=1e-06)
assert_allclose(points[::2, 1], 0.0, atol=1e-06)
assert points[2, 0] > 0
assert points[0, 0] < 0
assert_allclose(points[1, 0], 0.0, atol=1e-06)
assert points[1, 1] > 0
fname_out = tmp_path / 'test-dig.fif'
make_dig_montage(lpa=fids[0]['r'], nasion=fids[1]['r'], rpa=fids[2]['r'], coord_frame='mri_voxel').save(fname_out, overwrite=True)
fids_2, coord_frame_2 = read_fiducials(fname_out)
assert coord_frame_2 == FIFF.FIFFV_MNE_COORD_MRI_VOXEL
assert_allclose([fid['r'] for fid in fids[:3]], [fid['r'] for fid in fids_2], rtol=1e-06)
assert coord_frame_2 is not None
```

## Next Steps


---

*Source: test_montage.py:156 | Complexity: Advanced | Last updated: 2026-05-18*