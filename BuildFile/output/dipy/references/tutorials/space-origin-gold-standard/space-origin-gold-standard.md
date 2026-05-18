# How To: Space Origin Gold Standard

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test space origin gold standard

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
# Fixtures: space, origin
```

## Step-by-Step Guide

### Step 1: Assign fname = value

```python
fname = FILEPATH_DIX[f'gs_mesh_{space.value.lower()}_{origin.value.lower()}.ply']
```

### Step 2: Assign sfs = load_surface(...)

```python
sfs = load_surface(fname, FILEPATH_DIX['gs_volume.nii'], from_space=space, from_origin=origin, to_space=space, to_origin=origin)
```

### Step 3: Assign vertices = np.loadtxt(...)

```python
vertices = np.loadtxt(fname.with_suffix('.txt'))
```

### Step 4: Assign faces = np.loadtxt(...)

```python
faces = np.loadtxt(FILEPATH_DIX['gs_mesh_faces.txt'])
```

### Step 5: Call npt.assert_allclose()

```python
npt.assert_allclose(vertices, sfs.vertices, atol=0.001, rtol=1e-06)
```

### Step 6: Call npt.assert_allclose()

```python
npt.assert_allclose(faces, sfs.faces, atol=0.001, rtol=1e-06)
```

### Step 7: Call sfs.to_rasmm()

```python
sfs.to_rasmm()
```

### Step 8: Call sfs.to_center()

```python
sfs.to_center()
```

### Step 9: Assign vertices = np.loadtxt(...)

```python
vertices = np.loadtxt(FILEPATH_DIX['gs_mesh_rasmm_center.txt'])
```

### Step 10: Call npt.assert_allclose()

```python
npt.assert_allclose(vertices, sfs.vertices, atol=0.001, rtol=1e-06)
```


## Complete Example

```python
# Setup
# Fixtures: space, origin

# Workflow
fname = FILEPATH_DIX[f'gs_mesh_{space.value.lower()}_{origin.value.lower()}.ply']
sfs = load_surface(fname, FILEPATH_DIX['gs_volume.nii'], from_space=space, from_origin=origin, to_space=space, to_origin=origin)
vertices = np.loadtxt(fname.with_suffix('.txt'))
faces = np.loadtxt(FILEPATH_DIX['gs_mesh_faces.txt'])
npt.assert_allclose(vertices, sfs.vertices, atol=0.001, rtol=1e-06)
npt.assert_allclose(faces, sfs.faces, atol=0.001, rtol=1e-06)
sfs.to_rasmm()
sfs.to_center()
vertices = np.loadtxt(FILEPATH_DIX['gs_mesh_rasmm_center.txt'])
npt.assert_allclose(vertices, sfs.vertices, atol=0.001, rtol=1e-06)
```

## Next Steps


---

*Source: test_stateful_surface.py:245 | Complexity: Advanced | Last updated: 2026-05-18*