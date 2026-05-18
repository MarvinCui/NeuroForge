# How To: Gifti Matching Space

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test gifti matching space

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `pathlib`
- `tempfile`
- `urllib.error`
- `nibabel`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.data`
- `dipy.io.surface`
- `dipy.io.utils`
- `dipy.utils.optpkg`

**Setup Required:**
```python
# Fixtures: type, fname, space, origin
```

## Step-by-Step Guide

### Step 1: Assign sfs = load_surface(...)

```python
sfs = load_surface(FILEPATH_DIX[fname], FILEPATH_DIX['anat.nii.gz'])
```

### Step 2: Call sfs.to_rasmm()

```python
sfs.to_rasmm()
```

### Step 3: Call sfs.to_center()

```python
sfs.to_center()
```

### Step 4: Assign ref_vertices = sfs.vertices.copy(...)

```python
ref_vertices = sfs.vertices.copy()
```

### Step 5: Call save_surface()

```python
save_surface(sfs, Path(tmpdir) / 'tmp.gii', to_space=space, to_origin=origin)
```

### Step 6: Assign sfs = load_surface(...)

```python
sfs = load_surface(Path(tmpdir) / 'tmp.gii', FILEPATH_DIX['anat.nii.gz'], from_space=space, from_origin=origin)
```

### Step 7: Call sfs.to_rasmm()

```python
sfs.to_rasmm()
```

### Step 8: Call sfs.to_center()

```python
sfs.to_center()
```

### Step 9: Assign save_vertices = sfs.vertices.copy(...)

```python
save_vertices = sfs.vertices.copy()
```

### Step 10: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(ref_vertices, save_vertices, decimal=5)
```


## Complete Example

```python
# Setup
# Fixtures: type, fname, space, origin

# Workflow
if type == 'gzip_base64':
    fname += '.gz'
sfs = load_surface(FILEPATH_DIX[fname], FILEPATH_DIX['anat.nii.gz'])
sfs.to_rasmm()
sfs.to_center()
ref_vertices = sfs.vertices.copy()
with TemporaryDirectory() as tmpdir:
    save_surface(sfs, Path(tmpdir) / 'tmp.gii', to_space=space, to_origin=origin)
    sfs = load_surface(Path(tmpdir) / 'tmp.gii', FILEPATH_DIX['anat.nii.gz'], from_space=space, from_origin=origin)
    sfs.to_rasmm()
    sfs.to_center()
    save_vertices = sfs.vertices.copy()
    npt.assert_almost_equal(ref_vertices, save_vertices, decimal=5)
```

## Next Steps


---

*Source: test_surface.py:92 | Complexity: Advanced | Last updated: 2026-05-18*