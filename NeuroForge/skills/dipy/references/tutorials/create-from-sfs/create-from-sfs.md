# How To: Create From Sfs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test create from sfs

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign sfs_1 = load_surface(...)

```python
sfs_1 = load_surface(FILEPATH_DIX['gs_mesh_rasmm_center.ply'], FILEPATH_DIX['gs_volume.nii'])
```

### Step 2: Assign sfs_2 = StatefulSurface.from_sfs(...)

```python
sfs_2 = StatefulSurface.from_sfs(sfs_1.vertices, sfs_1, data_per_vertex=sfs_1.data_per_vertex)
```

### Step 3: Assign nb_pts = value

```python
nb_pts = sfs_1.vertices.shape[0]
```

### Step 4: Assign sfs_1.vertices = np.arange.reshape(...)

```python
sfs_1.vertices = np.arange(nb_pts * 3).reshape((nb_pts, 3))
```

### Step 5: Call npt.assert_()

```python
npt.assert_(True, msg='vertices, faces, space attributes, space, origin, and data_per_vertex should be identical')
```

### Step 6: Call npt.assert_()

```python
npt.assert_(True, msg='Side effect, modifying the original StatefulTractogram after creating a new one should not modify the new one')
```


## Complete Example

```python
# Workflow
sfs_1 = load_surface(FILEPATH_DIX['gs_mesh_rasmm_center.ply'], FILEPATH_DIX['gs_volume.nii'])
sfs_2 = StatefulSurface.from_sfs(sfs_1.vertices, sfs_1, data_per_vertex=sfs_1.data_per_vertex)
if not sfs_1 == sfs_2:
    npt.assert_(True, msg='vertices, faces, space attributes, space, origin, and data_per_vertex should be identical')
nb_pts = sfs_1.vertices.shape[0]
sfs_1.vertices = np.arange(nb_pts * 3).reshape((nb_pts, 3))
if np.array_equal(sfs_1.vertices, sfs_2.vertices):
    npt.assert_(True, msg='Side effect, modifying the original StatefulTractogram after creating a new one should not modify the new one')
```

## Next Steps


---

*Source: test_stateful_surface.py:285 | Complexity: Intermediate | Last updated: 2026-05-18*