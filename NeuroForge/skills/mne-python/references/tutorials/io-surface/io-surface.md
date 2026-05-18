# How To: Io Surface

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test reading and writing of Freesurfer surface mesh files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading and writing of Freesurfer surface mesh files.'

```python
'Test reading and writing of Freesurfer surface mesh files.'
```

**Verification:**
```python
assert_array_equal(pts, c_pts)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert_array_equal(tri, c_tri)
```

### Step 3: Assign fname_quad = value

```python
fname_quad = data_path / 'subjects' / 'bert' / 'surf' / 'lh.inflated.nofix'
```

**Verification:**
```python
assert_equal(object_diff(vol_info, c_vol_info), '')
```

### Step 4: Assign fname_tri = value

```python
fname_tri = data_path / 'subjects' / 'sample' / 'bem' / 'inner_skull.surf'
```

**Verification:**
```python
assert_array_equal(pts, c_pts)
```

### Step 5: Assign fname_patch = value

```python
fname_patch = data_path / 'subjects' / 'fsaverage' / 'surf' / 'rh.cortex.patch.flat'
```

**Verification:**
```python
assert_array_equal(tri, c_tri)
```

### Step 6: Call _read_patch()

```python
_read_patch(fname_patch)
```

### Step 7: Call write_surface()

```python
write_surface(tmp_path / 'tmp', pts, tri, volume_info=vol_info, overwrite=True)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(pts, c_pts)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(tri, c_tri)
```

### Step 10: Call assert_equal()

```python
assert_equal(object_diff(vol_info, c_vol_info), '')
```

### Step 11: Call write_surface()

```python
write_surface(tmp_path / 'tmp.obj', pts, tri, volume_info=None, overwrite=True)
```

### Step 12: Assign unknown = read_surface(...)

```python
c_pts, c_tri = read_surface(tmp_path / 'tmp.obj', read_metadata=False)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(pts, c_pts)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(tri, c_tri)
```

### Step 15: Assign unknown = read_surface(...)

```python
pts, tri, vol_info = read_surface(fname, read_metadata=True)
```

### Step 16: Assign unknown = read_surface(...)

```python
c_pts, c_tri, c_vol_info = read_surface(tmp_path / 'tmp', read_metadata=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading and writing of Freesurfer surface mesh files.'
pytest.importorskip('nibabel')
fname_quad = data_path / 'subjects' / 'bert' / 'surf' / 'lh.inflated.nofix'
fname_tri = data_path / 'subjects' / 'sample' / 'bem' / 'inner_skull.surf'
for fname in (fname_quad, fname_tri):
    with _record_warnings():
        pts, tri, vol_info = read_surface(fname, read_metadata=True)
    write_surface(tmp_path / 'tmp', pts, tri, volume_info=vol_info, overwrite=True)
    with _record_warnings():
        c_pts, c_tri, c_vol_info = read_surface(tmp_path / 'tmp', read_metadata=True)
    assert_array_equal(pts, c_pts)
    assert_array_equal(tri, c_tri)
    assert_equal(object_diff(vol_info, c_vol_info), '')
    if fname != fname_tri:
        continue
    write_surface(tmp_path / 'tmp.obj', pts, tri, volume_info=None, overwrite=True)
    c_pts, c_tri = read_surface(tmp_path / 'tmp.obj', read_metadata=False)
    assert_array_equal(pts, c_pts)
    assert_array_equal(tri, c_tri)
fname_patch = data_path / 'subjects' / 'fsaverage' / 'surf' / 'rh.cortex.patch.flat'
_read_patch(fname_patch)
```

## Next Steps


---

*Source: test_surface.py:127 | Complexity: Advanced | Last updated: 2026-05-18*