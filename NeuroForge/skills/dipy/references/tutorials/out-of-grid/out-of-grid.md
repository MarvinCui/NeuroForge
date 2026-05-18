# How To: Out Of Grid

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test out of grid

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `os.path`
- `tempfile`
- `urllib.error`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.data`
- `dipy.io.stateful_surface`
- `dipy.io.surface`
- `dipy.io.utils`
- `dipy.utils.optpkg`

**Setup Required:**
```python
# Fixtures: value, is_out_of_grid
```

## Step-by-Step Guide

### Step 1: Assign sfs = load_surface(...)

```python
sfs = load_surface(FILEPATH_DIX['naf_lh.pial'], FILEPATH_DIX['naf_mni_masked.nii.gz'])
```

### Step 2: Call sfs.to_vox()

```python
sfs.to_vox()
```

### Step 3: Call sfs.to_corner()

```python
sfs.to_corner()
```

### Step 4: Assign tmp_vertices = sfs.vertices.copy(...)

```python
tmp_vertices = sfs.vertices.copy()
```

### Step 5: Assign sfs.vertices = tmp_vertices

```python
sfs.vertices = tmp_vertices
```

### Step 6: Call npt.assert_()

```python
npt.assert_(sfs.is_bbox_in_vox_valid() != is_out_of_grid)
```

### Step 7: Call npt.assert_()

```python
npt.assert_(False)
```


## Complete Example

```python
# Setup
# Fixtures: value, is_out_of_grid

# Workflow
sfs = load_surface(FILEPATH_DIX['naf_lh.pial'], FILEPATH_DIX['naf_mni_masked.nii.gz'])
sfs.to_vox()
sfs.to_corner()
tmp_vertices = sfs.vertices.copy()
tmp_vertices[0] += value
try:
    sfs.vertices = tmp_vertices
    npt.assert_(sfs.is_bbox_in_vox_valid() != is_out_of_grid)
except (TypeError, ValueError):
    npt.assert_(False)
```

## Next Steps


---

*Source: test_stateful_surface.py:168 | Complexity: Advanced | Last updated: 2026-05-18*