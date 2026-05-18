# How To: Equivalent Gii

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test equivalent gii

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

### Step 1: Assign fname = value

```python
fname = FILEPATH_DIX['gs_mesh.gii']
```

### Step 2: Assign sfs = load_surface(...)

```python
sfs = load_surface(fname, FILEPATH_DIX['gs_volume.nii'])
```

### Step 3: Assign faces = np.loadtxt(...)

```python
faces = np.loadtxt(FILEPATH_DIX['gs_mesh_faces.txt'])
```

### Step 4: Call npt.assert_allclose()

```python
npt.assert_allclose(faces, sfs.faces, atol=0.001, rtol=1e-06)
```

### Step 5: Call sfs.to_rasmm()

```python
sfs.to_rasmm()
```

### Step 6: Call sfs.to_center()

```python
sfs.to_center()
```

### Step 7: Assign vertices = np.loadtxt(...)

```python
vertices = np.loadtxt(FILEPATH_DIX['gs_mesh_rasmm_center.txt'])
```

### Step 8: Call npt.assert_allclose()

```python
npt.assert_allclose(vertices, sfs.vertices, atol=0.001, rtol=1e-06)
```


## Complete Example

```python
# Workflow
fname = FILEPATH_DIX['gs_mesh.gii']
sfs = load_surface(fname, FILEPATH_DIX['gs_volume.nii'])
faces = np.loadtxt(FILEPATH_DIX['gs_mesh_faces.txt'])
npt.assert_allclose(faces, sfs.faces, atol=0.001, rtol=1e-06)
sfs.to_rasmm()
sfs.to_center()
vertices = np.loadtxt(FILEPATH_DIX['gs_mesh_rasmm_center.txt'])
npt.assert_allclose(vertices, sfs.vertices, atol=0.001, rtol=1e-06)
```

## Next Steps


---

*Source: test_stateful_surface.py:269 | Complexity: Advanced | Last updated: 2026-05-18*